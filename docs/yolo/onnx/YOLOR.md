# YOLOR usage

##

### Convert model

#### 1. Download the YOLOR repo and install the requirements

```
git clone https://github.com/WongKinYiu/yolor.git
cd yolor
pip3 install -r requirements.txt
pip3 install onnx onnxsim onnxruntime
```

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_yolor.py` file from `models-convertion/yolo/onnx` directory to the `yolor` folder.

#### 3. Download the model

Download the `pt` file from [YOLOR](https://github.com/WongKinYiu/yolor) repo.

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file

- Main branch

  Example for YOLOR-CSP

  ```
  python3 export_yolor.py -w yolor_csp.pt -c cfg/yolor_csp.cfg --dynamic
  ```

- Paper branch

  Example for YOLOR-P6

  ```
  python3 export_yolor.py -w yolor-p6.pt --dynamic
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

#### 5. Upload the generated ONNX file

On [Lumeo's Console](https://console.lumeo.com/) click `Design -> AI Models -> Add model` and fill the form using those settings:

**Types & Weights tab**
* Format: `ONNX Lumeo YOLO`
* Capability: `Detection`
* Architecture: `YOLOR`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `0.0039215698` (click in `1/256`)
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`


