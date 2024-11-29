# lora训练可以替代全参数训练！

设矩阵 $M\in \mathbb{R} ^{m\times n}$ 的秩为$l$，且$\alpha_1 ,\alpha_2, \cdots , \alpha_l$为一组线性无关列向量（$\alpha_i \in \mathbb{R} ^{m\times 1}$）。

令$A=[ \alpha_1 ,\alpha_2, \cdots , \alpha_l]\in \mathbb{R} ^{m\times l}$，则存在$B\in \mathbb{R} ^{l\times n}$，使得

$$M = AB$$

取$\beta_i \in \mathbb{R} ^{1\times n}$为B的第$i$行，则$B=\begin{bmatrix} \beta_1\\ \beta_2\\ \vdots \\ \beta_l\\ \end{bmatrix}$，即

$$M = AB = \sum_{i=1}^{l} \alpha_i\beta_i$$

取$A_j=[ \alpha_{j\cdot r + 1} ,\alpha_{j\cdot r + 2}, \cdots , \alpha_{j\cdot r + r}]\in \mathbb{R} ^{m\times r}$，$B_j=\begin{bmatrix} \beta_{j\cdot r + 1}\\ \beta_{j\cdot r + 1}\\ \vdots \\ \beta_{j\cdot r + r}\\ \end{bmatrix}\in \mathbb{R} ^{r\times n}$，则

$$M = AB = \sum_{i=1}^{l} \alpha_i\beta_i = \sum_{j=0}^{\frac{l}{r}-1}(\sum_{i=1}^{r} \alpha_{j\cdot r + i}\beta_{j\cdot r + i}) = \sum_{j=0}^{\frac{l}{r}-1}A_iB_i$$

因此，任意$m\times n$ 阶矩阵都可以拆成$\frac{l}{r}$组r阶低秩矩阵乘积$A_iB_i$之和。

也就是说，**全参数微调可以由**$\frac{l}{r}$**次lora微调完全替代！** 最重要的是，这说明模型训练过程中也**可以由多次lora训练代替全参数训练！** 而且由于梯度下降是一个迭代性的过程，多次lora逼近目标所需的迭代次数并不一定会比全参数训练的迭代次数多多少！（把lora训练中得到的$A_iB_i$加到模型原始参数上算作一次lora训练，每次lora训练之后可以重新初始化$A_i和B_i$。）
