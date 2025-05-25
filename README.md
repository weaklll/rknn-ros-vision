
# RKNN-YOLOv5-ROS Integration on RK3588/RK3568

This project provides a complete C++-based real-time object detection pipeline utilizing Rockchip RK3588 and RK3568 SoMs (System on Modules). It integrates YOLOv5 models optimized for RKNN inference and is seamlessly interfaced with the ROS (Robot Operating System) framework for flexible deployment in robotics or embedded vision applications.

## 🚀 Project Overview

- **Platform**: Rockchip RK3588 / RK3568
- **Model**: YOLOv5 (custom-processed C3 and activation layers)
- **Model Format**: PyTorch → ONNX → RKNN
- **Inference**: RKNN SDK with NPU acceleration
- **Framework**: ROS (Robot Operating System)
- **Language**: C++
- **Image Source**: USB cameras via `usb-cam` ROS package
- **Performance**: Achieves up to **170 FPS at 640×640 resolution** using RK3588 with NPU multi-threaded inference.

## 🧠 Key Features

- 🔧 **Preprocessed YOLOv5**:
  - Modified C3 module and activation functions for RKNN compatibility.
  - Optimized export pipeline from PyTorch to ONNX to RKNN.

- ⚡ **NPU Acceleration**:
  - Fully utilizes the **Rockchip NPU** (not CUDA/GPU).
  - Supports asynchronous thread pool scheduling across 3 NPU cores.
  - Configurable up to 12 inference threads. Beyond 12 threads, NPU utilization reaches ~97%.
  - Overclocking is supported for further performance boost.

- 📦 **Integrated OpenCV**:
  - No need to compile OpenCV from source.
  - `librknnrt.so` is included.
  - Optionally uses either:
    - Fast and accurate **RGA-based resizing** (recommended, with kernel patch instructions provided).
    - Fallback to OpenCV-based `resize()` for compatibility.

- 🧩 **ROS Integration**:
  - Image input via `usb-cam`.
  - Outputs detection results and confidence scores as ROS messages.
  - Easily extendable for downstream tasks (e.g., tracking, robot actuation, SLAM).

## 🛠️ Requirements

- **Operating System**: Ubuntu (recommended 20.04 or above)
- **Development Board**: RK3588 / RK3568 with NPU
- **Dependencies**:
  - ROS (e.g., Noetic or Melodic)
  - `usb-cam` ROS package
  - Rockchip RKNN Toolkit
  - Provided `librknnrt.so` (already embedded)
  - OpenCV (linked, no external compilation required)

## ⚙️ RGA Compatibility Note

Some default demonstration systems on Rockchip boards may lack proper RGA driver support. This project provides:

1. **RGA kernel patch guide** (recommended).
2. **Fallback OpenCV resize implementation**.

We strongly suggest enabling RGA for the best performance and accuracy.

## 📈 Performance Benchmark

| Resolution | FPS   | Threads | NPU Usage |
|------------|--------|---------|------------|
| 640×640    | 170+  | 12      | ~97%      |

*Tested on RK3588 using multi-threaded asynchronous inference.*

## 📚 Acknowledgements

Special thanks to the open-source pioneers in the Rockchip developer community for their contributions to RKNN deployment and ROS integration. This project would not be possible without your foundational work.

We are proud to be part of this vibrant and supportive ecosystem.

## 🤝 Contribution

Contributions, suggestions, and PRs are welcome! Whether it's improving performance, expanding compatibility, or refining integration, we look forward to collaborating with you.

## 📜 License

This project is released under the MIT License.
