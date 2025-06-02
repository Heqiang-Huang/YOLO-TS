# YOLO-TS: Real-Time Traffic Sign Detection with Enhanced Accuracy Using Optimized Receptive Fields and Anchor-Free Fusion (IEEE TITS submitted)

 Junzhou Chen, Heqiang Huang, Ronghui Zhang, Nengchao Lyu, Yanyong Guo, Hong-Ning Dai, Hong Yan

[Paper Download](https://arxiv.org/pdf/2410.17144v1)

> **Abstract:** *Ensuring safety in both autonomous driving and advanced driver-assistance systems (ADAS) depends critically on the efficient deployment of traffic sign recognition technology. While current methods show effectiveness, they often compromise between speed and accuracy. To address this issue, we present a novel real-time and efficient road sign detection network, YOLO-TS. This network significantly improves performance by optimizing the receptive fields of multi-scale feature maps to align more closely with the size distribution of traffic signs in various datasets. Moreover, our innovative feature-fusion strategy, leveraging the flexibility of Anchor-Free methods, allows for multi-scale object detection on a high-resolution feature map abundant in contextual information, achieving remarkable enhancements in both accuracy and speed. To mitigate the adverse effects of the grid pattern caused by dilated convolutions on the detection of smaller objects, we have devised a unique module that not only mitigates this grid effect but also widens the receptive field to encompass an extensive range of spatial contextual information, thus boosting the efficiency of information usage. Furthermore, to address the scarcity of traffic sign datasets in adverse weather conditions, we have generated an anomaly-based road sign detection dataset, the Generated-TT100K-weather dataset, based on the TT100K dataset. Evaluation on challenging public datasets, TT100K, CCTSDB2021, as well as our generated Generated-TT100K-weather dataset, demonstrates that YOLO-TS surpasses existing state-of-the-art methods in terms of both accuracy and speed.*

## Method
![Flowchart](fig/Flowchart.jpg)
Application Scenarios of Traffic Sign Detection in Autonomous Driving.

![network](fig/network.png)
**YOLO-TS architecture.** The structure of YOLO-TS.

## Datasets
* The download link for the dataset is below:
<table>
<thead>
  <tr>
    <th>Datsets</th>
    <th>TT100K</th>
    <th>CCTSDB2021</th>
    <th>GTSDB</th>
    <th>Generated-TT100K-weather</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th>Download</th>
    <th> <a href="https://pan.quark.cn/s/24062830411b">Download (PDkS)</a> </th>
    <th> <a href="https://pan.quark.cn/s/ea20e9bfb364">Download (XTy3)</a> </th>
    <th> <a href="https://pan.quark.cn/s/b4b672efc69b">Download (xkND)</a> </th>
    <th> <a href="https://pan.quark.cn/s/eb6c18fb4ec5">Download (is1U)</a> </th>
  </tr>
</tbody>
</table>

* The file structure of the downloaded dataset is as follows.

```
datasets
├── TT100K
│   ├── train
│   └── test
├── CCTSDB2021
│   ├── train
│   ├── val
│   └── Classification based on weather and environment
│       ├── cloud
│       ├── foggy
│       ├── cloud
│       ├── night
│       ├── rain
│       ├── snow
│       ├── sunny
├── GTSDB
│   ├── train
│   └── val
├── Generated-TT100K-weather
    ├── train
    ├── test
    └── Classification based on weather and environment
        ├── night-test
        ├── rain-test
```

## Requirements
* To install requirements: 
```
pip install -r requirements.txt
```

## (Optional: If you are training your own dataset.) 
### Get n1,n2,n3,n4,n5 and Replace them in YOLO-TS.yaml
* Replace the path in calculate_depth.py with the path to your dataset's training set, and name it txt_name.
* Run python calculate_depth.py to obtain n1~n5.
* Replace n1~n5 in the backbone section of YOLO-TS.yaml with the values obtained in step 2.

## Usage
### Python

YOLO may also be used directly in a Python environment, and accepts the same [arguments](https://docs.ultralytics.com/usage/cfg/) as in the CLI example above:

```python
from ultralytics import YOLO

if __name__ == '__main__':

    # Load a model
    model = YOLO("./YOLO-TS_TT100K.yaml")  # or model = YOLO("./best.pt")

    # Train the model
    model.train(data="./TT100K-2016.yaml", epochs=200, batch=48, imgsz=640, device='0,1,2,3') # GTSDB use imgsz=1024

    # Evaluate model performance on the validation set
    metrics = model.val(data="./TT100K-2016.yaml", imgsz=640, batch=1, device='0') # GTSDB use imgsz=1024

    # Export the model to ONNX format
    path = model.export(format="engine", device='0', half=True, opset=12)
```

See YOLO [Python Docs](https://docs.ultralytics.com/usage/python/) for more examples.

## Experiment result
![result1](fig/result1.png)

## Pre-trained Models
The trained weight files for different datasets are listed below, including both `.pth` and `.trt` formats.

<table>
<thead>
  <tr>
    <th>Weights</th>
    <th>ckpt</th>
    <th>tensorrt</th>
  </tr>
</thead>
<tbody>
  <tr>
    <th>Quark Cloud</th>
    <th colspan="2"> <a href="https://pan.quark.cn/s/6a3002dfaab0">Download (MQC4)</a> </th>
  </tr>
</tbody>
</table>

## Citation
If you use YOLO-TS, please consider citing:
```
@article{chen2024yolo,
  title={YOLO-TS: Real-Time Traffic Sign Detection with Enhanced Accuracy Using Optimized Receptive Fields and Anchor-Free Fusion},
  author={Chen, Junzhou and Huang, Heqiang and Zhang, Ronghui and Lyu, Nengchao and Guo, Yanyong and Dai, Hong-Ning and Yan, Hong},
  journal={arXiv preprint arXiv:2410.17144},
  year={2024}
}
```

## Contact
Should you have any question or suggestion, please contact huanghq77@mail2.sysu.edu.cn
