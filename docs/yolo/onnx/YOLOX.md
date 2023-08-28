# YOLOX usage

**NOTE**: You can use the main branch of the YOLOX repo to convert all model versions.

##

### Convert model

#### 1. Download the YOLOX repo and install the requirements

```
git clone https://github.com/Megvii-BaseDetection/YOLOX.git
cd YOLOX
pip3 install -r requirements.txt
python3 setup.py develop
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_yolox.py` file from `models-convertion/yolo/onnx` directory to the `YOLOX` folder.

#### 3. Download the model

Download the `pth` file from [YOLOX](https://github.com/Megvii-BaseDetection/YOLOX/releases/) releases (example for YOLOX-s)

```
wget https://github.com/Megvii-BaseDetection/YOLOX/releases/download/0.1.1rc0/yolox_s.pth
```

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file (example for YOLOX-s)

```
python3 export_yolox.py -w yolox_s.pth -c exps/default/yolox_s.py --dynamic
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

**NOTE**: The default opset is 11.

```
--opset 12
```

#### 5. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `YOLOX`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `1.0`
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
