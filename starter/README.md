# Computer Pointer Controller

This project is meat to enable the control over the computer pointer through gaze detection from a video or webcam stream. 

[alt text](https://github.com/SHOROUKAWWAD/gaze-estimation-pointer-controller/edit/master/starter/pic.png "modelpic")
#### possible uses 
 it can be a very helpful tool for people with disabilities in their forelimbs 

## Project Set Up and Installation
 To be able to run this project or make use of it, you will need to install Intel distribution of OpenVINO toolkit 

see the [guide](https://docs.openvinotoolkit.org/latest/)

for linux:

	git clone https://github.com/SHOROUKAWWAD/gaze-estimation-pointer-controller

## Demo
*TODO:* Explain how to run a basic demo of your model.

## Documentation
### Downloading models 
To download the models using OpenVino downloader tool:

		cd mouse-controller 
		python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "face-detection-adas-binary-0001"

######for landmarks-regression-retail-0009	
		cd mouse-controller 
		python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "landmarks-regression-retail-0009"

######for head-pose-estimation-adas-0001
		cd mouse-controller 
		python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "head-pose-estimation-adas-0001"

#####for gaze-estimation-adas-0002
		cd mouse-controller 
		python3 /opt/intel/openvino/deployment_tools/tools/model_downloader/downloader.py --name "gaze-estimation-adas-0002"
	

### Running commands

#### CPU

		python3 main.py -f ../../intel/face-detection-adas-binary-0001/<percision>/face-detection-adas-binary-0001.xml -fl ../../intel/landmarks-regression-retail-0009/<percision>/landmarks-regression-retail-0009.xml -hp ../../intel/head-pose-estimation-adas-0001/<percision>/head-pose-estimation-adas-0001.xml -g ../../intel/gaze-estimation-adas-0002/<percision>/gaze-estimation-adas-0002.xml  -i ../bin/demo.mp4 -d CPU -flags fd fld hp ge

#### GPU 
		python3 main.py -f ../../intel/face-detection-adas-binary-0001/<percision>/face-detection-adas-binary-0001.xml -fl ../../intel/landmarks-regression-retail-0009/<percision>/landmarks-regression-retail-0009.xml -hp ../../intel/head-pose-estimation-adas-0001/<percision>/head-pose-estimation-adas-0001.xml -g ../../intel/gaze-estimation-adas-0002/<percision>/gaze-estimation-adas-0002.xml  -i ../bin/demo.mp4 -d CPU -flags fd fld hp ge

#### FPGA

		python3 main.py -f ../../intel/face-detection-adas-binary-0001/<percision>/face-detection-adas-binary-0001.xml -fl ../../intel/landmarks-regression-retail-0009/<percision>/landmarks-regression-retail-0009.xml -hp ../../intel/head-pose-estimation-adas-0001/<percision>/head-pose-estimation-adas-0001.xml -g ../../intel/gaze-estimation-adas-0002/<percision>/gaze-estimation-adas-0002.xml  -i ../bin/demo.mp4 -d HETERO:CPU,FPGA -flags fd fld hp ge

#### VPU : NCS2

		python3 main.py -f ../../intel/face-detection-adas-binary-0001/<percision>FP32-INT1/face-detection-adas-binary-0001.xml -fl ../../intel/landmarks-regression-retail-0009/<percision>/landmarks-regression-retail-0009.xml -hp ../../intel/head-pose-estimation-adas-0001/<percision>/head-pose-estimation-adas-0001.xml -g ../../intel/gaze-estimation-adas-0002/<percision>/gaze-estimation-adas-0002.xml  -i ../bin/demo.mp4 -d MYRIAD -flags fd fld hp ge

### Arguments:

	-f : path to the xml  face detection model file  

	-fl : path to the xml  facial landmarks  detection model file

	-hp : path to the xml  headpose estimation model file

	-g  : path to the xml gaze estimation xml model file 

	-d  : device name (CPU, GPU,FPGA,VPU,..etc)

	-flags : the bounding boxes for the model you want to display  params (fd: facedetection , fld faciallandmarks detection, hp: head pose estimation, ge : gaze estimation)
 
## Benchmarks
with FP32:
laod time : 0.55
total inference time: 3.68
FPS: 16.3 ~ 16 

with FP16 :  
laod time : 0.64
total inference time: 3.41
FPS: 17.59 ~ 18 

with INT8 :
laod time : 1.19
total inference time: 3.19
FPS: 18.8 ~ 19 
## structure 
.
├── intel
│   ├── face-detection-adas-binary-0001
│   │   └── FP32-INT1
│   │       ├── face-detection-adas-binary-0001.bin
│   │       └── face-detection-adas-binary-0001.xml
│   ├── gaze-estimation-adas-0002
│   │   ├── FP16
│   │   │   ├── gaze-estimation-adas-0002.bin
│   │   │   └── gaze-estimation-adas-0002.xml
│   │   ├── FP16-INT8
│   │   │   ├── gaze-estimation-adas-0002.bin
│   │   │   └── gaze-estimation-adas-0002.xml
│   │   └── FP32
│   │       ├── gaze-estimation-adas-0002.bin
│   │       └── gaze-estimation-adas-0002.xml
│   ├── head-pose-estimation-adas-0001
│   │   ├── FP16
│   │   │   ├── head-pose-estimation-adas-0001.bin
│   │   │   └── head-pose-estimation-adas-0001.xml
│   │   ├── FP16-INT8
│   │   │   ├── head-pose-estimation-adas-0001.bin
│   │   │   └── head-pose-estimation-adas-0001.xml
│   │   └── FP32
│   │       ├── head-pose-estimation-adas-0001.bin
│   │       └── head-pose-estimation-adas-0001.xml
│   └── landmarks-regression-retail-0009
│       ├── FP16
│       │   ├── landmarks-regression-retail-0009.bin
│       │   └── landmarks-regression-retail-0009.xml
│       ├── FP16-INT8
│       │   ├── landmarks-regression-retail-0009.bin
│       │   └── landmarks-regression-retail-0009.xml
│       └── FP32
│           ├── landmarks-regression-retail-0009.bin
│           └── landmarks-regression-retail-0009.xml
└── starter
    ├── bin
    │   └── demo.mp4
    ├── README.md
    ├── requirements.txt
    └── src
        ├── face_detection.py
        ├── facial_landmarks_detection.py
        ├── gaze_estimation.py
        ├── head_pose_estimation.py
        ├── input_feeder.py
        ├── main.py
        ├── mouse_controller.py
        └── __pycache__
            ├── face_detection.cpython-37.pyc
            ├── facial_landmarks_detection.cpython-37.pyc
            ├── gaze_estimation.cpython-37.pyc
            ├── head_pose_estimation.cpython-37.pyc
            ├── input_feeder.cpython-37.pyc
            └── mouse_controller.cpython-37.pyc

## Results

The reduction of the model size due to the reduction of percision reduces the inference time. However, reducing the percision affects the accuracy of the model. 

