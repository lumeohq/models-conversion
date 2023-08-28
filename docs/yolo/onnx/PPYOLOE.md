# PP-YOLOE / PP-YOLOE+ usage

**NOTE**: You can use the release/2.6 branch of the PPYOLOE repo to convert all model versions.

##

### Convert model

#### 1. Download the PaddleDetection repo and install the requirements

https://github.com/PaddlePaddle/PaddleDetection/blob/release/2.6/docs/tutorials/INSTALL.md

**NOTE**: It is recommended to use Python virtualenv.

#### 2. Copy conversor

Copy the `export_ppyoloe.py` file from `models-convertion/yolo/onnx` directory to the `PaddleDetection` folder.

#### 3. Download the model

Download the `pdparams` file from [PP-YOLOE](https://github.com/PaddlePaddle/PaddleDetection/tree/release/2.6/configs/ppyoloe) releases (example for PP-YOLOE+_s)

```
wget https://paddledet.bj.bcebos.com/models/ppyoloe_plus_crn_s_80e_coco.pdparams
```

**NOTE**: You can use instead your trained model weights.

#### 4. Convert model

Generate the ONNX model file (example for PP-YOLOE+_s)

```
pip3 install onnx onnxsim onnxruntime
python3 export_ppyoloe.py -w ppyoloe_plus_crn_s_80e_coco.pdparams -c configs/ppyoloe/ppyoloe_plus_crn_s_80e_coco.yml --dynamic
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
* Architecture: `PP-YOLOE`
* Labels: Type the labels or import the labels file (each line represents a different model's class)
* Weights: Upload the previously generated ONNX file

**Parameters tab**
* Net scale factor: `0.0173520735727919486`
* Color format: `RGB`
* Network precision: `Float16`
* Clustering algorithm: `NMS`
