首先，我们考虑观测变量与潜在变量线性相关的模型，但是潜在概率分布不是高斯分布。这种模型的一个重要的类别被称为独立成分分析（independent component analysis），或者ICA。 如果我们考虑潜在变量上的概率分布的分解，即    

$$
p(z) = \sum\limits_{j=1}^Mp(z_j) \tag{12.89}
$$    

那么我们就会应用到这个模型。为了理解这种模型的作用，考虑这样一个场景：两个人同时讲话，我们使用两个麦克风来记录他们的声音。如果我们忽略诸如时间延迟和回声之类的影响，那么在任意时间点，麦克风接收到的信号都是两个声音的振幅的线性组合。这个线性组合的系数是常数，并且如果我们可以从采样数据中推断它们的值，那么我们就可以将混合的过程（假设非奇异）进行求逆，从而得到两个干净的信号，每个信号只包含一个人的声音。这是盲源划分（blind source separation）问题的一个例子，其中，“盲”表示我们只给定了混合数据，而原始 的数据源和混合系数都没有被观测到（Cardoso， 1998）。    

这类问题有时使用下面的方法解决（MacKay， 2003），其中我们忽略信号的时序本质，将连续的样本看成是独立同分布的。我们考虑一个生成式模型，其中有两个潜在变量，对应于未观测的语音信号的幅值，有两个观测变量，由麦克风的信号值给定。潜在变量的联合概率分布可以按照上面的方式分解，观测变量由潜在变量的线性组合给定。我们无需引入一个噪声分布，因为潜在变量的数量等于观测变量的数量，从而观测变量的边缘概率分布通常不会是奇异的，因此观测变量仅仅由潜在变量的线性组合确定。给定一组观测数据，模型的似然函数是线性组合的系数的一个函数。对数似然函数可以使用基于梯度的最优化方法进行最大化，得到了独立 成分分析的一个特定的版本。    

这种方法的成功需要令潜在变量具有非高斯的概率分布。为了说明这一点，回忆一下在概率PCA（以及因子分析）中，潜在空间分布是一个零均值的各向同性的高斯分布。于是，模型 无法区分那些区别仅仅在于潜在空间的旋转的潜在变量的不同选择。这一点可以用下面的方法直接验证：我们注意到边缘概率密度（12.35）在变换$$ W \to WR $$下是不变的，因此似然函数也是不变的，其中$$ R $$是正交矩阵，满足$$ RR^T = I
$$，这是因为式（12.36）给出的矩阵$$ C $$本身是不变的。将这个模型进行扩展，使得更多的概率潜在分布被包含到模型中，结论不会改变，因为正如我们已经看到的那样，这种模型等价于零均值各向同性的高斯潜在变量模型。    

我们用另一种方式说明为什么线性模型中的高斯潜在变量分布对于找到独立的成分是不够的。我们注意到，主成分表示数据空间中的坐标系的一个旋转，从而对协方差矩阵进行了对角化，因此新的坐标系中的数据分布没有相关性。虽然不具有相关性是独立性的一个必要条件，但是它不是充分条件。在实际应用中，潜在变量分布的一个常见的选择是    

$$
p(z_j) = \frac{1}{\pi cosh(z_j)} = \frac{2}{\pi(e^{z_j} + e^{-z_j})} \tag{12.90}
$$    

这与高斯分布相比，具有长尾的性质，这反映了许多现实世界中的概率分布同样具有这种性质。    

最初的ICA模型（Bell and Sejnowski， 1995）基于的是由信息最大化定义的目标函数的最优化过程。概率潜在变量形式的一个优点是它有助于对基本ICA的推广进行形式化描述。例如，独立因子分析（independent factor
analysis）研究的是这样的模型：潜在变量的数量和观测变量的数量可以不同，观测变量带有噪声，各个潜在变量的概率分布很灵活，由混合高斯模型建模。这个模型的对数似然函数使用EM算法进行最大化，潜在变量的重建使用变分方法进行近似。研究者们也在研究许多其他类型的模型，现在有许多文献研究ICA及其应用（Jutten and Herault， 1991; Comon et al.， 1991; Amari et al.， 1996; Pearlmutter and Parra， 1997; Hyvarinen Oja， 1997; Hinton et al.， 2001; Miskin and MacKay， 2001; Hojen-Sorensen et al.， 2002; Choudrey and Roberts， 2003; Chan et al.， 2003; Stone， 2004）。