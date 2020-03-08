## Pyramid Scene Parsing Network[[paper]()][[code](https://github.com/hszhao/semseg)]



### 概要
- Context取得をmulti-scaleで行うPyramid Pooling Moduleの提案
- 補助lossの導入による性能の改善(現在ではデファクトと言って良い)
- 2017年時点では多くのデータセットでSOTAを達成しており，Segmentationのレベルを１段上に上げた立役者

![psp1](./psp/psp1.jpg)

### 手法
- BackBone  
ResNetのblock3,4にdilationを入れたDilated ResNetを使用
- Pyramid Pooling Module
  - ParseNetではGlobal Average Pooling１つでContextを取得
  - PPMはそれをmulti-scaleでcascadeしたもの  
  - ADE20Kのようにバリエーションの豊富なデータセットではmulti-scaleの効果が得られる  
  (ParseNetとさほど性能が変わらないという結果も見たことがあるが)
- Deep Super Vision
  - 深いネットワークで勾配を上流まで伝播させる工夫
  - ResNetのblock3から予測を出力しLossに加える
  - 推論時には不要
![psp2](./psp/psp2.jpg)

### 結果
- Cityscapes，ADE20KでSOTA

### 採択会議
CVPR2017

tag: dsemantic segmentation, context, scene parsing