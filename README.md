Introduction
---------

OpenCV itself can show a bitmap using `imshow()` function but in a wxWidgets
application one may want to display a bitmap acquired with OpenCV using wxWidgets GUI.
The most convenient class for doing that in wxWidgets is `wxBitmap`.

Project wxOpenCVTest presents function
```cpp
bool ConvertMatBitmapTowxBitmap(const cv::Mat& matBitmap, wxBitmap& bitmap);
```
which converts an OpenCV bitmap encoded as BGR CV_8UC3 (the most common format) to a `wxBitmap`.

The function comes with a simple program which uses OpenCV and wxWidgets to acquire
and display bitmaps coming from several sources: image file, video file, default webcam,
and IP camera. The program also benchmarks how long a bitmap took to acquire, convert, and display.
The program can be built using a provided CMakeFile.


Tested on MS Windows 10 only, with wxWidgets 3.1.5 and OpenCV 4.4 using MSVC (64-bit, MSVS 2017 and 2019)
and GCC (32-bit, mingw-w64-i686-toolchain with GCC 10.2).

Please read the comments in `convertmattowxbmp.h`, they contain useful and perhaps surprising information
(e.g., how much slower the debug version of the generic convert function is on MSW).


How to use
---------
1. Add files `convertmattowxbmp.h` and `convertmattowxbmp.cpp` to your project.
2. Include `convertmattowxbmp.h` where needed.
3. Call `ConvertMatBitmapTowxBitmap()` as described in the comments in `convertmattowxbmp.h`.


Notes
---------
After closing a debug build of a wxWidgets application linking to OpenCV DLL
(via import library `opencv_world440d.lib`), MSVS reports many memory leaks,
even in the simplest possible application just declaring a `cv::Mat` variable
without ever touching it or calling any OpenCV function. No such leaks are there
for pure Win32 application equivalent. I found similar reports on the internet,
but no conclusive solution or even explanation.

Surprisingly, OpenCV does not really support Unicode paths, see for example
https://github.com/opencv/opencv/issues/4292#issuecomment-601686965 for more information.


Licence
---------
[wxWidgets licence](https://github.com/wxWidgets/wxWidgets/blob/master/docs/licence.txt)