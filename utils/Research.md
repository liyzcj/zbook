# Research

### Abstract: 终端设备上的 机器学习  



## 分析为什么要在终端设备上部署机器学习

- #### 机器学习的重要性

  - [独立于云的嵌入式智能iphone](https://diginomica.com/2017/11/21/embedded-deep-learning-out-of-the-cloud-and-onto-devices/)
  - [介绍机器学习](http://www.opengardensblog.futuretext.com/archives/2015/05/an-introduction-to-deep-learning-and-its-role-for-iot-future-cities.html)
  - [云雾互联，不仅仅在云端](https://www.iotforall.com/intelligent-iot-fog-computing-trends/)

- #### 机器学习对物联网的影响

  - ~~[计算机视觉与物联网，计算机视觉与深度学习](https://strategyofthings.io/iot-computer-vision)~~

  - [确定多个传感器对决定的影响需要机器学习](https://internetofthingsagenda.techtarget.com/blog/IoT-Agenda/Smarter-IoT-applications-incorporate-machine-learning)  边缘计算的重要性

  - ~~[Machine Learning Make IoT Devices Safe](https://www.greycampus.com/blog/big-data/machine-learning-for-a-stronger-iot-security-environment)~~ 

  - ~~[机器学习的工业物联网应用](https://www.computerweekly.com/news/450431977/How-machine-learning-is-applied-in-industrial-IoT)~~

  - [The roles of cloud computing and fog computing in the Internet of Things revolution](http://www.businessinsider.com/internet-of-things-cloud-computing-2016-10)

- #### 实例[物联网和分布机器学习优化推荐系统](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=7562703) 

- #### 传统大互联——机器学习让我们更好地管理物联网

  - https://www.forbes.com/sites/marcochiappetta/2018/03/27/nvidia-and-arm-partnership-to-bring-deep-learning-technology-to-iot-devices/#585abaff7520 理解物联网设备语言
  - 边缘深度学习可以减少云服务数据入口的流量， 从而节约大量成本https://conferences.oreilly.com/oscon/oscon-or/public/schedule/detail/67199
  - [google cloud](https://cloud.google.com/solutions/automating-iot-machine-learning) 云端训练并传输模型

## 能不能在终端设备上部署机器学习

- #### 硬件

  - https://www.businessinsider.de/arm-and-nvidia-eye-deep-learning-in-the-iot-2018-3?r=US&IR=T 英伟达， arm

  - https://www.forbes.com/sites/marcochiappetta/2018/03/27/nvidia-and-arm-partnership-to-bring-deep-learning-technology-to-iot-devices/#585abaff7520 英伟达， arm

  - [NVIDIA and ARM want to bring deep learning to your IoT projects](https://www.techrepublic.com/article/nvidia-and-arm-want-to-bring-deep-learning-to-your-iot-projects/)

- #### 软件

  - ~~[可能性与实现](https://www.researchgate.net/post/Can_IoT_applications_benefit_from_deep_learning_architectures_at_their_resource-constrained_devices)~~
  - 每个终端设备每秒 都产生成千上万的数据——有数据基础
  - [Bringing deep learning to IoT devices](http://samsungnext.com/whats-next/deep-learning-iot/)
  - [嵌入式深度学习：走出云端，进入设备](https://diginomica.com/2017/11/21/embedded-deep-learning-out-of-the-cloud-and-onto-devices/)

## 怎么样在终端设备实现机器学习和深度学习

- [开源边缘计算project flogo](https://www.flogo.io/)
- [Machine Learning at the Edge](https://www.ugent.be/ea/idlab/en/research/ai-for-robotics-and-iot/machine-learning-at-the-edge.htm)
- [gluon](https://zh.gluon.ai/index.html)  https://www.engineering.com/IOT/ArticleID/15827/Deep-Learning-Tools-for-IoT-Are-Released-in-an-Open-Source-Library.aspx
- [apache](https://github.com/apache/incubator-mxnet)
- [edgeML:implement on strawberry](https://www.microsoft.com/en-us/research/project/resource-efficient-ml-for-the-edge-and-endpoint-iot-devices/) 

## 终端实现机器学习的结果

## 性能评估

## 观点	

- 机器学习的关键是需要大数据，并且数据要有一定的格式，最好是被标注过的， 物联网完美的复合这一点， 想象整个地球上的无数物联网设备遵循某一协议而生成的相同规格的数据， 为深度学习提供数据基础，再将训练后的模型运用到无数的设备中，那将是一个智能的时代。

- Sure you can. I just trained an AlexNet on a server then took the model and implememted it on a respberry pi 2. The classification on the pi take less than 100ms. We also trained a GoogleNet and tried it on the pi, it took 30 seconds per classification. Now we are upgrading to pi 3 with gpu capabilities. __from 【可能性与实现】

## 贯穿全文的paper

- [Enabling Deep Learning on IoT Devices](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8057306)
- [Machine learning for Internet of Things data analysis: A survey]()
- [Analysis of Eight Data Mining Algorithms for Smarter Internet of Things (IoT)](https://ac.els-cdn.com/S187705091632213X/1-s2.0-S187705091632213X-main.pdf?_tid=68251758-67fa-4925-838a-792a7ff8289e&acdnat=1528982865_848f05805f6ba57068c257350ab195da)
- [Edge computing technologies for Internet of Things: a primer](https://reader.elsevier.com/reader/sd/16E059C8CAC000CA66E2EDF55A93AB9BAED514E53FBB2FEF81A2B2DA1836E1BFAD47D8504813DB4857B3A7F16ADA6BCC)
- [Deep Learning for IoT Big Data and Streaming Analytics: A Survey](https://arxiv.org/pdf/1712.04301.pdf) 

## 最终项目-树莓派物体识别 发送到手机

- [How to easily Detect Objects with Deep Learning on Raspberry Pi](https://medium.com/nanonets/how-to-easily-detect-objects-with-deep-learning-on-raspberrypi-225f29635c74)
- [Accelerating Convolutional Neural Networks on Raspberry Pi](http://cv-tricks.com/artificial-intelligence/deep-learning/accelerating-convolutional-neural-networks-on-raspberry-pi/)
- [You Only Look Once: Unified, Real-Time Object Detection](https://pjreddie.com/media/files/papers/yolo_1.pdf)
- [SSD: Single Shot MultiBox Detector](https://arxiv.org/abs/1512.02325)
