## 比赛网址

[2018 Atrial Segmentation Challenge](http://atriaseg2018.cardiacatlas.org/)

## 总结论文

[A Global Benchmark of Algorithms for Segmenting Late Gadolinium-Enhanced Cardiac Magnetic Resonance Imaging](https://www.researchgate.net/publication/341178287_A_Global_Benchmark_of_Algorithms_for_Segmenting_Late_Gadolinium-Enhanced_Cardiac_Magnetic_Resonance_Imaging)

## 简介

* 目的：使用深度学习完成LGE MRI上的左心房分割

* 数据量：100个训练数据，54个测试数据（label未公开）

* 其他信息：数据尺寸为（576，576，88）和（640，640，88），分辨率：$0.625\times 0.625\times 0.625\, mm^3$ ，二腔心。

* 标注规则：LA腔体标签将LA心内膜、二尖瓣以及左心耳、肺静脉包含在内。肺静脉的长度不超过 $10\, mm$ 或者心肌厚度的三倍（未公开心肌厚度数据），停止原则是半径小于指定阈值。

* 数据格式：nrrd，数据为灰度数据（灰度值不超过255，大部分灰度值低于100），标签为二值数据 $\{0\, ,255\}$ 

## 评价指标

  在3D数据上计算指标，A代表预测结果，B代表ground truth，==以Dice Score为排名标准==。

  Dice Score：像素级衡量指标
$$
Dice =\frac{2|A\cap B|}{|A|+|B|}
$$


  IoU/Jaccard Index：衡量二者的相似性
$$
IoU=\frac{|A\cap B|}{|A\cup B|}
$$


  Sensitivity、specificity：衡量模型的敏感度与特异性，(TP, True Positive; TN: True Negative; FP: False Positive; FN: False Negative)
$$
  Sensitivity=\frac{TP}{TP+FN}\\
  Specificity=\frac{TN}{TN+FP}
$$
  Hausdorff Distance（HD）：衡量两个面之间的局部最大距离，可以用来衡量几何相似性，a、b代表属于预测结果A和标签B的像素
$$
  HD = max_{b\in B}\{min_{a\in A}\{\sqrt{a^2-b^2}\}\}
$$


  Surface to Surface Distance （STSD）：衡量两个面之间的平均距离误差 $n_{*}$ 属于 $*$ 的像素个数， $p / p'$ 属于A或B的所有点
$$
  STSD=\frac{1}{n_A+n_B}(\sum_{p=1}^{n_A}\sqrt{p^2-B^2}+\sum_{p'=1}^{n_B}\sqrt{p'^2-A^2})
$$

LA anterior-posterior diameter：计算每一个scan中LA从前到后的最大欧式距离，单位 $mm$ 。

3D LA volume：所有LA像素的总数，单位 $cm^3$ 。

## 结论

==本部分均为组织者根据提交的论文总结的结论，仅供参考==

参赛并提交论文共17支队伍，其中15支使用CNN效果明显优于其他2支，2D和3D网络没有明显差异；UNet网络效果优于FCN和ResNet；使用级联的CNN（先定位再分割）效果会有提升，定位越准分割结果越好，但是当ROI小于240*160时由于心房的边界过于接近ROI边界导致分割结果变差