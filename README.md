# opencv_gpu_video_reader

This is an OpenCV example, where `video_reader.cpp` is taken directly from `opencv/samples/gpu` and whipped into shape where it actually builds and runs.

The sample demonstrates performance improvement gained from using NVIDIA codec with OpenCV.

## Code Modifications

In order to port this functionality to your application (as well as make the actual OpenCV sample run):

1. Add `dynlink_nvcuvid.cpp` to your source
2. Include the following:

```cpp 
#include <dynlink_nvcuvid.h>
````

3. Use the following code to initialize NVCUVID

```cpp
using namespace std;

// Init CUDA
void *hHandleDriver = nullptr;
CUresult cuda_res = cuInit(0, __CUDA_API_VERSION, hHandleDriver);
if (cuda_res != CUDA_SUCCESS)
{
    throw exception();
}
cuda_res = cuvidInit(0);
if (cuda_res != CUDA_SUCCESS)
{
    throw exception();
}

```

## Building and Running

### Prerequeisits

1. Ubuntu 16.04 +
2. CUDA 9.0 +
3. [OpenCV 3.3+](https://docs.opencv.org/3.4/d2/de6/tutorial_py_setup_in_ubuntu.html)
4. [OpenGL](http://www.codebind.com/linux-tutorials/install-opengl-ubuntu-linux/) (optional, if you want to watch the video)
5. [OpenGL hooks for GTK](https://stackoverflow.com/questions/34697700/opengl-support-with-opencv-3-0/37951922)

It is not necessary to install OpenGL, if not installing just comment out any UX-related lines in `video_reader.cpp`

### Build
```sh
git clone https://github.com/fierval/opencv_gpu_video_reader.git
cd opencv_gpu_video_reader
mkdir build
cd build
cmake ..
make
```

### Run

```sh
./vider_reader <path_to_a_video>

```

### Results



