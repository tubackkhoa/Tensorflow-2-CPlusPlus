# tensorflow-object-detection-cpp

A C++ example of running TensorFlow Object Detection model in live mode.
Inspired by [issue](https://github.com/tensorflow/models/issues/1741#issuecomment-318613222).

Requirements (for use without Bazel):

- `TensorFlow` .so builds ([more](https://github.com/tensorflow/tensorflow/issues/2412#issuecomment-300628873), requires Bazel to build)
- `Eigen3` headers ([more](http://eigen.tuxfamily.org/index.php?title=Main_Page))
- `OpenCV` ([more](https://github.com/opencv/opencv))

Usage:

1. Specify your own paths for necessary libs in `CmakeLists.txt`
2. Specify your own paths for `frozen_inference_graph.pb` and `labels_map.pbtxt` in `main.cpp` (lines 44-47)
3. Specify your video source (`main.cpp`, line 80)
4. Have fun

![DEMO](demo.png)

## Tensorflow build

```bash
# C++
./configure
bazel build //tensorflow:libtensorflow_cc.so

# copy to system
mkdir /usr/local/include/tf
cp -r bazel-genfiles /usr/local/include/tf/
cp -r tensorflow /usr/local/include/tf/
cp -r third_party /usr/local/include/tf/
cp bazel-bin/tensorflow/libtensorflow_* /usr/local/lib/
```
