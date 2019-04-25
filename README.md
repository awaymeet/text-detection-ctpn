# text-detection-ctpn

基于ctpn的场景文本检测（连接文本提议网络）。 它在tensorflow中实现。 原始文件可以在[这里]（https://arxiv.org/abs/1609.03605）找到。 另外，caffe中的原始回购可以在[here]（https://github.com/tianzhi0549/CTPN）中找到。 有关论文和代码的更多详细信息，请参阅[blog]（http://slade-ruan.me/2017/10/22/text-detection-ctpn/）。 如果您有任何疑问，请先检查问题，如果问题仍然存在，请打开新问题。
***
**
NOTICE: 
**
***
# 路线图
- [x] reonstruct the repo
- [x] cython nms and bbox utils
- [x] loss function as referred in paper
- [x] oriented text connector
- [x] BLSTM
***
# 安装
nms和bbox utils是用cython编写的，因此你必须先构建库。
```shell
cd utils/bbox
chmod +x make.sh
./make.sh
```
它将在当前文件夹中生成nms.so和bbox.so。
***
# 例子
- follow setup to build the library 
- download the ckpt file from [googl drive](https://drive.google.com/file/d/1HcZuB_MHqsKhKEKpfF1pEU85CYy4OlWO/view?usp=sharing) or [baidu yun](https://pan.baidu.com/s/1BNHt_9fiqRPGmEXPaxaFXw)
- put checkpoints_mlt/ in text-detection-ctpn/
- put your images in data/demo, the results will be saved in data/res, and run demo in the root 
```shell
python ./main/demo.py
```
***
# 训练
## 准备数据
- First, download the pre-trained model of VGG net and put it in data/vgg_16.ckpt. you can download it from [tensorflow/models](https://github.com/tensorflow/models/tree/1af55e018eebce03fb61bba9959a04672536107d/research/slim)
- Second, download the dataset we prepared from [google drive](https://drive.google.com/file/d/1npxA_pcEvIa4c42rho1HgnfJ7tamThSy/view?usp=sharing) or [baidu yun](https://pan.baidu.com/s/1nbbCZwlHdgAI20_P9uw9LQ). put the downloaded data in data/dataset/mlt, then start the training.
- Also, you can prepare your own dataset according to the following steps. 
- Modify the DATA_FOLDER and OUTPUT in utils/prepare/split_label.py according to your dataset. And run split_label.py in the root
```shell
python ./utils/prepare/split_label.py
```
- it will generate the prepared data in data/dataset/
- The input file format demo of split_label.py can be found in [gt_img_859.txt](https://github.com/eragonruan/text-detection-ctpn/blob/banjin-dev/data/readme/gt_img_859.txt). And the output file of split_label.py is [img_859.txt](https://github.com/eragonruan/text-detection-ctpn/blob/banjin-dev/data/readme/img_859.txt). A demo image of the prepared data is shown below.
<img src="/data/readme/demo_split.png" width=640 height=480 />

***
## 训练 
Simplely run
```shell
python ./main/train.py
```
- checkpoints_mlt中提供的模型在GTX1070上针对50k iters进行了训练。 每次大约需要0.25秒。 因此完成50k迭代需要大约3.5小时。
***
# some results
`NOTICE:` 下面使用的所有照片都是从互联网上收集的。 如果它对您有影响，请与我联系删除它们。
<img src="/data/res/006.jpg" width=320 height=480 /><img src="/data/res/008.jpg" width=320 height=480 />
<img src="/data/res/009.jpg" width=320 height=480 /><img src="/data/res/010.png" width=320 height=320 />
***
## 面向文本连接器
- 面向文本连接器已经实现，我正在工作，但仍需要进一步改进。
- 左图是DETECT_MODE H的结果，右图是DETECT_MODE O.
<img src="/data/res/007.jpg" width=320 height=240 /><img src="/data/res_oriented/007.jpg" width=320 height=240 />
<img src="/data/res/008.jpg" width=320 height=480 /><img src="/data/res_oriented/008.jpg" width=320 height=480 />
***
