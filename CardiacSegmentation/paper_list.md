# 心脏分割
* 论文题目：[Q. Dou et al., "PnP-AdaNet: Plug-and-Play Adversarial Domain Adaptation Network at Unpaired Cross-Modality Cardiac Segmentation," in IEEE Access, vol. 7, pp. 99065-99076, 2019, doi: 10.1109/ACCESS.2019.2929258.](https://ieeexplore.ieee.org/abstract/document/8764342)[CODE](https://github.com/carrenD/Medical-Cross-Modality-Domain-Adaptation)<br>
简介：MRI作为源域，CT作为目标域，分割网络作为生成器，设定feature-level和mask-level两个层级的判别器来判断feature/mask的来源<br>
* 论文题目：[Bian C, Yuan C, Wang J, et al. Uncertainty-aware Domain Alignment for Anatomical Structure Segmentation[J]. Medical Image Analysis, 2020: 101732.](https://www.sciencedirect.com/science/article/pii/S1361841520300967?casa_token=C3hxLdd_EEcAAAAA:ys_eViohA7rOp53bPPNb3dJpWY2eKW-kK2ORSRYfYNsBd2ybJtotOzp2sEpkeOgWfNgkCZf0Yw)<br>
简介：训练分三个阶段<br>
		1.使用自编码器作为先验网络学习源域数据的分布，然后使用源域数据和标签训练后验网络，最小化先验网络和后验网络的KL距离来优化先验网络。将先验网络学到的分布送入到分割网络中计算分割结果，通过M		次采样的均值计算不确定性并使用不确定性为分割损失加权。<br>
		2.使用预训练好的网络分割目标域，根据分割结果的不确定性对目标域数据从小到大排序，不确定性越大分割难度越大，按照课程学习策略从易到难自训练分割网络。<br>
		3.源域和目标域都送入到网络中，通过判别器判别数据来源于哪个域<br>
		Note:2和3交替训练，使用第2阶段简单样本的伪标签监督第3阶段目标域的分割。
		
