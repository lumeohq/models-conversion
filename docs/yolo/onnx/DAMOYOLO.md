# DAMO-YOLO usage

##

### Convert model

#### 1. Download the DAMO-YOLO repo and install the requirements

```
git clone https://github.com/tinyvision/DAMO-YOLO.git
cd DAMO-YOLO
pip3 install -r requirements.txt
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_damoyolo.py` file from `models-convertion/yolo/onnx` directory to the `DAMO-YOLO` folder.

#### 3. Download the model

Download the `pth` file from [DAMO-YOLO](https://github.com/tinyvision/DAMO-YOLO) releases (example for DAMO-YOLO-S*)

```
wget https://idstcv.oss-cn-zhangjiakou.aliyuncs.com/DAMO-YOLO/release_model/clean_model_0317/damoyolo_tinynasL25_S_477.pth
```

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file (example for DAMO-YOLO-S*)

```
python3 export_damoyolo.py -w damoyolo_tinynasL25_S_477.pth -c configs/damoyolo_tinynasL25_S.py --dynamic
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

**NOTE**: The default opset is 11.

```
--opset 11
```

#### 5. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `DAMO-YOLO`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `1.0`
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
