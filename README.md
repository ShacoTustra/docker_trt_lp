# LivePortrait on TensorRT from Docker
Simple way to start LivePortrait on TensorRT.

# Installation
Download image:
docker pull shacotustra/trt-lp

Run the container:
docker run -it --gpus=all \
--restart=always \
shacotustra/trt-lp \
/bin/bash

Check cuda availabilty inside the container:
nvcc --version
nvidia-smi

If cuda is not available:
ln -sf /usr/lib/x86_64-linux-gnu/libnvidia-ml.so.560.35.03 /usr/lib/x86_64-linux-gnu/libnvidia-ml.so.1
ln -sf /usr/lib/x86_64-linux-gnu/libcuda.so.560.35.03 /usr/lib/x86_64-linux-gnu/libcuda.so.1

Go to workspace:
cd /workspace

Convert ONNX to TensorRT (it may take some time):
sh scripts/all_onnx2trt.sh
sh scripts/all_onnx2trt_animal.sh

Try it:
python run.py \
 --src_image assets/examples/source/s1.jpg \
 --dri_video assets/examples/driving/d0.mp4
