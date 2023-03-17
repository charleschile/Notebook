# B站教程



## 【meta分析视频教程】基于R语言的meta分析

### 1. 基于r语言的meta分析

meta-analysis

对不同研究结果进行收集、合并及统计分析的方法

将以往的研究结果更为客观地总和反映出来

加权平均



#### 异质性

统计学异质性：

Q统计量以及I2统计量可以检验异质性（越大越异质）



#### 1. 选题

#### 2. 文献检索

MEDLINE, cochranne library, Ovid, embase, web of science, pubmed

pubmed MeSH主题词检索

#### 3. R作图

森林图、漏斗图、敏感性分析和亚组分析展示（药敏）





### 2. 传统意义上的meta分析在r上的实现

Q检验0.05

I2检验 40%？

fixed effect model 固定效应模型

random effect model 随机效应模型





### 3. 诊断性实验的meta分析在r中的实现







### 4. 如何用r做出偏倚风险评估图（ROB）







### 5. 如何用r语言实现累积meta分析













## 



## 系统性文献综述写作教程

### 1. 什么是文献综述





### 2. 为什么要写文献综述







### 3. 文献综述分类





### 4. 系统性综述是什么









### 5. 系统性综述怎么写







## 图书馆精准获取生物医学文献讲座

### 1. 场景目的

找到感兴趣、research gap，找到研究方向

The meta-analysis of exercise for osteoarthritis --- （求全）









### 2. 文献类型

图书馆馆藏资源

搜索引擎：google scholar



Meta-analysis需要高质量的实验文献









### 3. 获取方式



生物医学主要的数据库：pubmed, medline, embase, cbm（中国的pbmed）, web of science



pubmed 基本上会包含medline

embase和pubmed有部分交集

web of science（有核心等级，可以帮助我们筛选出高质量的期刊）







### 4. 检索方法

pubmed收录范围：medline, old-midline(1950-1965, 没有MeSH字段), pre-medline 



#### 1. 检索词的选择与扩充

自然语言检索 -- 自由词

人工语言检索 -- 主题词 （准确、而且搞定了同义词，但是有很多还没进行过MeSH标注的文章）







#### 2. 检索式的编制







#### 3. 检索方法的选择











#### 4. 检索策略的调整





## Dissertation: Meta-analysis of the relationship between male infertility and plasma entrogen and plasma androgen concentration



**also, the sperm count and the sperm quality**





关键词确定法：

male infertility

plasma entrogen, androgen



PICO确定法：

participant: male infertility

intervention

compare

 outcome











|      关键词      | 主题词 |                            自由词                            |
| :--------------: | :----: | :----------------------------------------------------------: |
| male infertility |        | aspermia, asthenozoospermia, azoospermia, oligospermia, sertoli Cell-Only Syndrome, teratozoospermia |
|   sperm count    |        |                                                              |
|    androgens     |        | dihydrotestosterone, nandrolone, oxandrolone, oxymetholone, stanozolol, testosterone |
|     estrogen     |        |                                                              |



#### 主题词确认

使用pubmed mesh database确认主题词



##### 关键词male infertility（https://www.ncbi.nlm.nih.gov/mesh/68007248）

MeSH主题词tree

Aspermia, Asthenozoospermia, Azoospermia, Oligospermia, Sertoli Cell-Only Syndrome, Teratozoospermia



##### 关键词sperm count （https://www.ncbi.nlm.nih.gov/mesh/68013076）

没有其他自由词





##### 关键词androgens （https://www.ncbi.nlm.nih.gov/mesh/68000728）

https://www.ncbi.nlm.nih.gov/mesh/82000728 （[Pharmacological Action]）

Dihydrotestosterone, Nandrolone, Oxandrolone, Oxymetholone, Stanozolol, Testosterone



##### 关键词estrogen （https://www.ncbi.nlm.nih.gov/mesh/68004967）

https://www.ncbi.nlm.nih.gov/mesh/82004967（[Pharmacological Action]）

Chlorotrianisene (MeSH Term)
Coumestrol (MeSH Term)
Dienestrol (MeSH Term)
Diethylstilbestrol (MeSH Term)
Epimestrol (MeSH Term)
Equol (MeSH Term)
Estradiol (MeSH Term)
Estrogenic Steroids, Alkylated (MeSH Term)
Estrogens, Conjugated (USP) (MeSH Term)
Estrogens, Esterified (USP) (MeSH Term)
Estrone (MeSH Term)
Ethinyl Estradiol (MeSH Term)
Genistein (MeSH Term)
Hexestrol (MeSH Term)
Mestranol (MeSH Term)
Quinestrol (MeSH Term)
Zearalenone (MeSH Term)
Zeranol (MeSH Term)



##### 关键词sperm count



((male infertility) OR (sperm count)) AND ((androgen) OR (estrogen))



(("Infertility, Male"[Mesh]) OR ("Sperm Count"[Mesh])) AND (("Androgens"[Mesh]) OR ("Androgens" [Pharmacological Action]) OR ("Estrogens"[Mesh]) OR ("Estrogens" [Pharmacological Action]))
