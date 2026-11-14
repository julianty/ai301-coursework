I fixed a bmp import bug in OpenImageIO. The issue was the import flow assumed a color mask order instead of reading it from the file's header. I was able to diagnose the issue with the help of a mantainer, implement a fix, test it, and opened a PR which merged a day later.

https://github.com/AcademySoftwareFoundation/OpenImageIO/pull/5650
