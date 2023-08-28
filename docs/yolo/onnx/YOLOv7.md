# YOLOv7 usage

**NOTE**: The yaml file is not required.

##

### Convert model

#### 1. Download the YOLOv7 repo and install the requirements

```
git clone https://github.com/WongKinYiu/yolov7.git
cd yolov7
pip3 install -r requirements.txt
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_yoloV7.py` file from `models-convertion/yolo/onnx` directory to the `yolov7` folder.

#### 3. Download the model

Download the `pt` file from [YOLOv7](https://github.com/WongKinYiu/yolov7/releases/) releases (example for YOLOv7)

```
wget https://github.com/WongKinYiu/yolov7/releases/download/v0.1/yolov7.pt
```

**NOTE**: You can use instead your trained model weights.

#### 4. Reparameterize your model

[YOLOv7](https://github.com/WongKinYiu/yolov7/releases/) and its variants cannot be directly converted to engine file. Therefore, you will have to reparameterize your model using the code [here](https://github.com/WongKinYiu/yolov7/blob/main/tools/reparameterization.ipynb). Make sure to convert your custom checkpoints in yolov7 repository, and then save your reparmeterized checkpoints for conversion in the next step.

#### 5. Convert model

Generate the ONNX model file (example for YOLOv7)

```
python3 export_yoloV7.py -w yolov7.pt --dynamic
```

**NOTE**: To convert a P6 model

```
--p6
```

**NOTE**: To change the inference size (defaut: 640 / 1280 for `--p6` models)

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

**NOTE**: The default opset is 12.

```
--opset 12
```

#### 6. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `YOLOv7`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `0.0039215698` (click in `1/256`)
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
