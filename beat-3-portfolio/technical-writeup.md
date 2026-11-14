# I fixed a .bmp import bug in OpenImageIO that scrambled image channels

## Overview

OpenImageIO is an open source image library. I wrote a fix for an old issue ([#1901](https://github.com/AcademySoftwareFoundation/OpenImageIO/issues/1901)) where a 32-bit .bmp file imported with its color channels out of order. With guidance from the maintainer, I found that the reader ignored the channel masks in the file's header and assumed a fixed byte order. I reproduced the bug on my machine, wrote a fix that reads each channel using its mask, added tests that demonstrate it, and opened [PR #5650](https://github.com/AcademySoftwareFoundation/OpenImageIO/pull/5650). The maintainer approved it and merged it about seven hours later, and the issue closed with the merge.

## What happened

The issue title said the A and B channels were swapped. I downloaded the issue's `input.bmp` and compared OpenImageIO against Pillow, a different image library. OpenImageIO read blue as 255 everywhere and alpha as varying, while Pillow read the opposite, so I posted that and said I would start with the narrow case.

The maintainer, lgritz, replied:

> I wonder if a deeper problem is lurking. I think what you want to do is carefully construct a test where the R, G, B, and A values are _different_ from each other in each pixel, so that you can clearly verify that the channels are in the right order, and that there are no other channel swappings that are going unnoticed.

I kept the header of `input.bmp` and filled every pixel with R=10, G=50, B=100, A=200. The result showed the bug was bigger than the title:

```
OIIO unique per channel:   [[50], [100], [200], [10]]
Pillow unique per channel: [[10], [50], [100], [200]]
```

All four channels were wrong, and the file was being read as G, B, A, R. The cause was in `bmpinput.cpp`. It swapped bytes 0 and 2 for every 24- and 32-bit file, which assumes B, G, R, A order. This file's header masks say the bytes are stored A, B, G, R, and swapping 0 and 2 of that gives G, B, A, R.

My fix adds a branch in `read_native_scanline` that applies each channel's mask and shift. It only runs for 32-bit `BI_BITFIELDS` files with V4 or V5 headers:

```cpp
if (m_dib_header.bpp == 32 && m_dib_header.compression == 3
    && (m_dib_header.size == WINDOWS_V4
        || m_dib_header.size == WINDOWS_V5)) {
    for (unsigned int i = 0, j = 0; j < scanline_bytes; i += 4, j += 4) {
        uint32_t pixel = *(uint32_t*)&fscanline[i];
        mscanline[j + 0] = (uint8_t)bit_range_convert(
            (pixel & m_dib_header.red_mask) >> m_right_shifts[0],
            m_bit_counts[0], 8);
        // ... green and blue the same way ...
        if (m_dib_header.alpha_mask == 0) {
            mscanline[j + 3] = 255;
        } else { /* alpha the same way */ }
    }
    return true;
}
```

I tested with two 2x2 files I built by hand with Python's `struct.pack`, `g32bf-rgba-v5.bmp` and `g32bf-noalpha-v5.bmp`, where every pixel and channel has a different value. I added both to `testsuite/bmp/run.py`.

### A change I made

My first version of the new branch was wrong in two ways. It had no `return true`, so it fell through into the old byte-swap code and the output was still scrambled. I also ran alpha through `bit_range_convert` like the other channels, which gives 0, fully transparent, when the alpha mask is 0 because the bit count is 0. I added the `return true` and the explicit `alpha_mask == 0` case that writes 255. After that, a copy of `distinct.bmp` with the alpha mask zeroed read as `10 50 100 255` on my branch (it read `50 100 200 10` on `main`), and that became the second regression file.

### How it ended

I opened the PR on 2026-11-03. A review bot recommended approval, and lgritz approved with "LGTM, thanks for the fix!" and merged it at 22:18 UTC, with all 30 checks passing. Issue #1901 closed with the merge. I did not need a second review round.

## Limitations and what's next

My fix does not cover 32-bit `BI_BITFIELDS` files with a V3 header and non-default masks. They are still misread, because the reader never loads the masks for V3 headers, and fixing that means changing `bmp_pvt.cpp`. I kept the change to V4 and V5 so it touched one source file, and I said so in the PR description.

Working on this taught me how BMP files store pixels (the V3, V4 and V5 headers and what a channel mask is), how to build and test a large C++ project, and how a PR works in a big project, including the sign-off and AI-disclosure rules.
