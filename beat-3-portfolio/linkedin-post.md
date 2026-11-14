I fixed a bug in OpenImageIO, an open source image library, where some .bmp pictures loaded with their colors scrambled. I worked out the cause with the project's maintainer, wrote the fix and its tests, and opened a pull request.

The problem: the file says which order its color values are stored in, but the library ignored that and assumed a standard order. For one kind of file, red, green, blue and transparency all came out in the wrong places.

How it ended: the maintainer approved the fix and merged it about seven hours after I opened it, and the original report from 2018 was closed.

What it taught me:
✅ Test with a different value in every channel. My first check hid how big the bug really was until the maintainer suggested it.
✅ My first fix was wrong, and my own tests caught it before anyone else saw it.
✅ I left one rarer file type out on purpose to keep the change small. It's still unfixed, and I plan to report it as a follow-up.

https://github.com/AcademySoftwareFoundation/OpenImageIO/pull/5650

#OpenSource #SoftwareEngineering #Testing
