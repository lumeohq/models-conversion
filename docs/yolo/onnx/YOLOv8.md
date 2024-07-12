# YOLOv8 usage

**NOTE**: The yaml file is not required.

##

### Convert model

#### 1. Install Ultralytics YOLOv8 and dependencies

```
pip3 install ultralytics[export]
pip3 install onnxsim cmake
```

**NOTE**: It is recommended to use Python virtualenv or the [Ultralytics container](https://github.com/ultralytics/yolov5/wiki/Docker-Quickstart)

#### 2. Clone the Lumeo models-conversion repository

```
git clone https://github.com/lumeohq/models-conversion
cd models-conversion
```

#### 3. Download the model

Download the `pt` file from [YOLOv8](https://github.com/ultralytics/assets/releases/) releases (example for YOLOv8s) to the "models-conversion" folder

```
wget https://github.com/ultralytics/assets/releases/download/v0.0.0/yolov8s.pt
```

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file (example for YOLOv8s)

```
python3 ./yolo/onnx/export_yoloV8.py -w yolov8s.pt --dynamic
```

**NOTE**: To change the inference size (defaut: 640)

```
-s SIZE
--size SIZE
-s HEIGHT WIDTH
--size HEIGHT WIDTH
```

Example for 1280

```
-s 1280
```

or

```
-s 1280 1280
```

**NOTE**: To simplify the ONNX model

```
--simplify
```

**NOTE**: To use dynamic batch-size

```
--dynamic
```

**NOTE**: To use implicit batch-size (example for batch-size = 4)

```
--batch 4
```

**NOTE**: The default opset is 16.

```
--opset 12
```

#### 5. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `YOLOv8`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `0.0039215698` (click in `1/256`)
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
