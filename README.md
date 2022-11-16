# Boundary-aware Backward-Compatible Representation via Adversarial Learning in Image Retrieval
## introduction
Backward-compatible training (BCT) aims to deploy a new model without the operation of "backfilling". We introduce AdvBCT, an Adversarial Backward-Compatible Training method with an elastic boundary constraint that takes both compatibility and discrimination into consideration. The codes for AdvBCT and the benchmark are all publicly available in this repo.
## Datasets
### Landmark
#### ROxford and RParis
* download revisted Oxford & Paris (http://cmp.felk.cvut.cz/revisitop/) into ./data/

   （don’t need download R-1M distractor dataset. gnd_roxford5k.pkl and gnd_rparis6k.pkl  are required)
* ./data structure
```bash
.
└── ROxfordParis
    ├── gnd_roxford5k.pkl
    ├── gnd_rparis6k.pkl
    ├── roxford5k
    │   └── jpg
    └── rparis6k
        └── jpg
```

#### GLDv2

## Enviroments
```bash
conda create -n bct python=3.7
conda activate bct
#conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
conda install faiss-cpu
pip install -r requirements.txt
```

## Evaluation
evaluate datasets on 32G v100

```bash
mkdir -p output/final_model
```
* move models to ./output/final_model/
Models can be download in [GDrive](https://drive.google.com/drive/folders/1sjlvFiEJTF2Zkt-Tal1KH-Gce_Wra9EH?usp=share_link). The password is our submitted ID.
* test
```bash
bash scripts/test.sh landmark roxford5k ./data/ROxfordParis/
bash scripts/test.sh landmark rparis6k ./data/ROxfordParis/
# take a long time
bash scripts/test.sh landmark gldv2 ./data/GLDv2
```

####  Results

| Allocation Type | old model | new model | RParis(self) |  RParis(cross) | ROxford(self) | ROxford(cross) |
| :------| :----| :------| :----| :----| :----| :----|
|Extended-class | $\phi_o^{R18}$|  $\phi_o^{R18}$ | 74.29 | - | 54.34 | - |
|Extended-class | $\phi_o^{R18}$|  $\phi_*^{R18}$ | 81.15 | 4.93 | 63.85 |1.20 |
|Extended-class | $\phi_o^{R18}$ | $\phi_{BCT}^{R18}$ |79.45|76.13|58.94|53.43|
|Extended-class | $\phi_o^{R18}$ | $\phi_{LCE}^{R18}$ |81.26 | 76.78| 60.49 | 54.29|
|Extended-class | $\phi_o^{R18}$ | $\phi_{UniBCT}^{R18}$ |76.92|74.55|59.07|57.82|
|Extended-class | $\phi_o^{R18}$ | $\phi_{Hot-refresh}^{R18}$ |78.93|75.33|60.31|51.68|
|Extended-class | $\phi_o^{R18}$ | $\phi_{AdvBCt}^{R18}$ |82.05 | 77.16 | 64.51 | 54.82|

### Next-step
The following content will also be released after paper acceptance.
- [ ] Release of preprocess codes for training datasets.
- [ ] Release of training codes for 5 works.
- [ ] Release of training codes for other task, such as person reid.

### License
The code is released under MIT license.
```plaintext
MIT License

Copyright (c) 2022 AdvBCT

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

