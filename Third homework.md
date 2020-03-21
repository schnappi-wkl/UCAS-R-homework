## T test

#### 1.单样本t检验
 		根据某地环境保护法规定，倾入河流的废水中某种有毒化学物质的平均含量不得超过3ppm。
该地区环保组织对沿河各厂进行采样，测定每日倾入河流中废水的含量某厂连续50天的检测记录:

~~~R
3.192384 2.705439 3.011549 3.183452 2.395339 2.902747 3.126290 2.793181 3.341457 2.493988
3.103322 3.194163 2.825478 3.068507 2.840561 2.873001 2.945115 2.732162 2.591894 2.886801
2.877525 2.794586 2.443543 3.591346 3.197254 3.933672 3.124787 2.873258 3.199061 3.010036
3.069658 2.702002 2.604343 3.209037 2.616383 3.006684 3.145670 3.643886 3.142165 3.137628
3.038345 2.855303 3.039129 1.987688 3.033372 3.174961 3.332280 2.419560 2.481433 2.828260
~~~

 		对数据进行正态性检验
~~~R
shapiro.test(x)
Shapiro-Wilk normality test
data: x W = 0.97007, p-value = 0.233
~~~
 		由p=0.233>0.05,我们有95%的把握认为数据服从正态分布，故我们可以进行单样本的t检验

 		为了判断是否符合环保标准，建立如下假设：

 											H0：μ≤3，H1：μ>3

~~~R
>t.test(x,mu=3)
One Sample t-test
t = -0.94718, df = 49, p-value = 0.3482
alternative hypothesis: true mean is not equal to 3
95 percent confidence interval:2.857634 3.051153
sample estimates:mean of x 2.954394 
~~~

由于p>0.05 故接受原假设，因此，在α=0.95的水平上认为该厂水质中的有毒物质达标

#### 2.配对T检验

 		某物质在化学处理前后的含脂率如下：
~~~R
before：0.19,0.18,0.21,0.30,0.66,0.42,0.08,0.12,0.30,0.27
after： 0.15,0.13,0.00,0.07,0.24,0.24,0.19,0.04,0.08,0.20
~~~

 		对数据进行正态性检验：

~~~R
> shapiro.test(before)
Shapiro-Wilk normality test
data: before W = 0.88457, p-value = 0.1472

> shapiro.test(after)
Shapiro-Wilk normality test
data: after W = 0.94236, p-value = 0.5795
~~~

 		两个样本的P均大于0.05,我们有95%把握认为两个样本的数据服从正态分布，故我们进行配对T检验

~~~R
> t.test(before,after,paired = TRUE)
Paired t-test
data:  before and after:t = 3.0373, df = 9, p-value = 0.01408
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:0.0354749 0.2425251
sample estimates:mean of the differences 0.139 
~~~

 		由于p<0.05 故接受原假设，因此，在α=0.05的水平上我们认为该物质在化学处理前后的含脂率发生了显著的变化，说明化学处理能显著降低该物质的含脂率。

#### 3.独立样本的T检验
 		为比较用来做鞋子后跟的两种材料的质量，选取了15名成年男子，每人穿一双新鞋，其中一只是用材料A做后跟的，另外一只是用材料B做后跟的，其厚度都是10mm，过了一个月后在测量厚度，试问两种材料是否一样耐穿？（取α=0.05）
~~~R
A：5.6,7.0,8.3,8.2,5.2,9.3,7.9,8.5,7.8,7.5,6.1,8.9,6.1,9.4,9.1
B：7.4,5.4,8.8,8.0,6.8,9.1,6.3,7.5,7.0,6.5,4.4,7.7,4.2,9.4,9.1
~~~

 		为了 检测数据的正态性，我们进行Shapiro-Wilk检验
~~~R
> shapiro.test(A)
Shapiro-Wilk normality test
data:  A W = 0.92737, p-value = 0.2492
> shapiro.test(B)
Shapiro-Wilk normality test
data:  B W = 0.94452, p-value = 0.4426

~~~

 		两个样本的P均大于0.05,我们有95%把握认为两个样本的数据服从正态分布，故我们进行配对T检验

~~~R
> t.test(A,B,var.equal = F)
Welch Two Sample t-test
data:  A and B:t = 0.88401, df = 27.22, p-value = 0.3844
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:-0.6424813  1.6158146
sample estimates:mean of x mean of y  7.660000  7.173333 
~~~

 		由于p>0.05 故接受原假设，因此，在α=0.95的水平上认为两种鞋底一样耐穿