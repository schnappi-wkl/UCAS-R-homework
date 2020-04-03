 ## 4th homework
 #### 题目
 		**某地调查3000名失业人员，按性别文化程度分类如下，试从α=0.05的水平上检验失业人员的性别与文化程度是否有关。**

|      | 大专以上 | 中专以上 | 高中 | 初中及一下 | 行和 |
| :--: | :------: | :------: | :--: | :--------: | :--: |
|  男  |    40    |   138    | 620  |    1043    | 1843 |
|  女  |    20    |    72    | 442  |    625     | 1159 |
| 列和 |    60    |   210    | 1062 |    1668    | 3000 |
#### 代码
如下：
~~~R
survey<-matrix(c(40,20,138,72,620,442,1043,625),nrow=2)
row=c("男","女")
column=c("大专以上","中专技校","高中","初中及一下")
dimnames(survey)=list(row,column)
chisq.test(survey)

	Pearson's Chi-squared test

data:  survey
X-squared = 7.332, df = 3, p-value = 0.06204

fisher.test(survey, alternative = "greater")

	Fisher's Exact Test for Count Data

data:  survey
p-value = 0.06378
alternative hypothesis: greater

qchisq(0.95,3)
 7.814728

~~~

本例中，r=2，c=3，在α=0.05下，

$$
\chi_{2}^{0.05}(r-1)(c-1)=\chi_{2}^{0.05}(3)=7.815
$$

故拒绝与为w={χ2 ≥7.815}

我们分别进行了卡方检验和Fisher精确度检验，χ2 =7.332≤7.815，从而在α=0.05水平上样本落入接受域，另外通过Fisher精确检验我们得出p=0.06378>0.05，接受原假设。总之我们认识失业人员的性别和文化程度无关。