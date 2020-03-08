### Title/Authors/link
Fully Convolutional Networks for Semantic Segmentation


### 概要
- Semantic SegmentationをCNNを用いて行った最初の論文
- 全結合層を用いず，全ての層をCNNで構成(Fully Convolutional Networks; FCN)することで，
pixel-wiseなクラス分類を行うことに成功
- 中間層の特徴(Mid-level)を活用することで，FineなSegmentationができることを示した

![fcn1]("./fcn/fcn1.png" "fcn1")


### 手法
- FCN(32s)の構成
  - 論文ではVGGをbackboneとして使用  
  全結合層よりも上流側については通常のVGGと同様．
  - 全結合層の畳み込み層による置換(1/32の解像度)
    1. クラス分類で用いられているVGGでは7*7*512 -> 4096という全結合層が使われている．
    2. これを入力チャンネル数が512，カーネルサイズが(7, 7)の畳み込み層で置換する．  
    ※当初のFCNはクラス分類モデルの影響を色濃く残し(7, 7)のカーネルを用いているが  
    それを(3, 3)にし出力チャンネル数も小さくしているものがスタンダードになっている．
  - ピクセル毎のクラス分類
    1. 入力の1/32の解像度でピクセル毎のクラス分類を行うネットワークを追加．
    2. 入力画像の解像度と合わせるために，Transposed Convolutionを用いてupsamplingする．  
    より手軽にbilinearでinterpolationしている場合もある．
- FCN16sの構成
  1. backboneの解像度1/16時点での特徴量を用いてクラス分類する．
  2. FCN32sの推論出力(1/32の解像度)を1/16のスケールまでupsamplingし，1/16の推論出力と足し合わせて最終出力とする．
- FCN8sの構成
  1. backboneの解像度1/8時点での特徴量を用いてクラス分類する．
  2. FCN16sの推論出力(1/16の解像度)を1/8のスケールまでupsamplingし，1/8の推論出力と足し合わせて最終出力とする．

![fcn2]("./fcn/fcn2.png" "fcn2")  
![fcn3]("./fcn/fcn3.png" "fcn3")

### 結果
- PASCAL VOC2012(test)でmIoU=62.2．
- 論文にはNYUDv2，SIFT-Flow，Pascal Contextの結果もあり．
![fcn4]("./fcn/fcn4.png" "fcn4")

