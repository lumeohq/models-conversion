# YOLO-NAS usage

**NOTE**: The yaml file is not required.

##

### Convert model

#### 1. Download the YOLO-NAS repo and install the requirements

```
git clone https://github.com/Deci-AI/super-gradients.git
cd super-gradients
pip3 install -r requirements.txt
python3 setup.py install
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_yolonas.py` file from `models-convertion/yolo/onnx` directory to the `super-gradients` folder.

#### 3. Download the model

Download the `pth` file from [YOLO-NAS](https://sghub.deci.ai/) releases (example for YOLO-NAS S)

```
wget https://sghub.deci.ai/models/yolo_nas_s_coco.pth
```

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file (example for YOLO-NAS S)

```
python3 export_yolonas.py -m yolo_nas_s -w yolo_nas_s_coco.pth --dynamic
```

**NOTE**: Model names

```
-m yolo_nas_s
```

or

```
-m yolo_nas_m
```

or

```
-m yolo_nas_l
```

**NOTE**: Number of classes (example for 80 classes)

```
-n 80
```

or

```
--classes 80
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

**NOTE**: The default opset is 14.

```
--opset 12
```

#### 5. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `YOLO-NAS`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `0.0039215698` (click in `1/256`)
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
