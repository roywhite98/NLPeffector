# 毕设-基因家族鉴定

## 葡萄霜霉菌NLP家族鉴定

### evalue为default = 10，未筛选
+ megablastn方法->[megablastnresult(2hits）](https://github.com/roywhite98/Atlanta/blob/dev/blast%E7%BB%93%E6%9E%9C/megablastnresult)
+ blastn方法->[blastnresult(7hits)](https://github.com/roywhite98/Atlanta/blob/dev/blast%E7%BB%93%E6%9E%9C/blastnresult)
+ tblastn方法->筛选掉evalue>0的序列(11hits-3hits)->[tblastnresult(8hits)](https://github.com/roywhite98/Atlanta/blob/dev/blast%E7%BB%93%E6%9E%9C/tblastnresult)
### 经比对发现，由于blast基于种子扩展算法，得出的序列很可能不完整，因此应该进行基因组注释（~~但是没有~~）
>+ 同源注释：下载几个其他代表性动植物的完整的蛋白集, 使用 TblastN 将蛋白序列比对到初步组装结果的序列上，E-value的阈值为1e-5. 将不同蛋白的BLAST的hits用 Solar 软件进行合并。GeneWise 根据每个BLAST hit的对应基因区域预测完整的基因结构。
>同源预测软件通常利用GeneWise和GeneMoMa，前者是需要同源物种的蛋白序列，后者需要同源物种基因组序列及对应的GFF文件，目前小编已经抛弃GeneWise，使用最多的就是GeneMoMa，但是让小编十分头疼的是在准备GFF文件太花费精力，这个软件真的是挑肥拣瘦，必须满足其格式才能可以运行，目前从NCBI的Reseq和Ensemble上下载都可以，其他地方来的那就得还点时间写个脚本改下了。
>+ 转录组预测：用Tophat将RNA-seq数据比对到初步组装结果的序列上，然后用cufflinks组装转录本形成基因模型。
>转录组数据预测PASA软件是基于Unigene/EST序列进行预测软件，这个可能就需要拿到一个混样转录组数据首先进行无参组装，接下来根据Unigene组装结果在进行比对，通常用Gmap或Blat两种方法，最好三代全长转录本和二代一起来进行预测，这样可以使得找到的结构更为准确、可靠，此外PASA还有另外的一个功能就是可以用其预测可变剪切，俗称PASA修饰。
>+ 从头预测：先构建repeat-mask genome， 在这个基础上就用 August, Genescan, GlimmerHMM, Geneid 和 SNAP 预测编码区
### 用TBtools预测ORF，配合tblastn结果->新鲜出炉的NLP序列
1. 新鲜出炉的NLP序列，提取DNA序列->[预测ORF+blast结果NLP基因](https://github.com/roywhite98/Atlanta/blob/dev/%E9%A2%84%E6%B5%8BORF%2Bblast%E7%BB%93%E6%9E%9CNLP%E5%9F%BA%E5%9B%A0.fa)
2. 使用megaX翻译序列->[预测ORF+blast结果NLP基因.AA.fas](https://github.com/roywhite98/Atlanta/blob/dev/%E9%A2%84%E6%B5%8BORF%2Bblast%E7%BB%93%E6%9E%9CNLP%E5%9F%BA%E5%9B%A0.AA.fas)
3. 使用Clustal Omega进行序列比对，使用Jalview美化->![鉴定的序列.png](https://github.com/roywhite98/Atlanta/blob/dev/%E9%89%B4%E5%AE%9A%E7%9A%84%E5%BA%8F%E5%88%97.png)
4. 使用SignalP5.0进行信号肽预测，使用SecretomeP2.0进行非经典分泌预测->[序列信息.xls](https://github.com/roywhite98/Atlanta/blob/dev/%E5%BA%8F%E5%88%97%E4%BF%A1%E6%81%AF.xlsx)


## ~~多卵菌NLP基因家族鉴定~~

### ~~NCBI搜集typeⅠ，typeⅡ，typeⅢ代表序列~~
+ ~~**typeⅢ** Afu5g02100 = XP_748132.1 conserved hypothetical protein \[Aspergillus fumigatus Af293\]~~
+ ~~**typeⅠ** PsojNIP = AAM48170.1 necrosis-inducing protein \[Phytophthora sojae\]~~
+ ~~**typeⅡ** NLPPcc = ACT13867.1 Necrosis inducing protein \[Pectobacterium carotovorum subsp. carotovorum PC1\]~~

### ~~进行blastp分析，做卵菌NLP序列准备~~
~~使用BlastP方法对nr数据库进行比对，取identify>=80%的序列，evalue小于1e-5的序列，并人工筛选在100aa到300aa的序列。  
得到了三个输出结果，并将其合并在[123汇总.fa](https://github.com/roywhite98/Atlanta/blob/dev/%E5%8D%B5%E8%8F%8Cblastp%E6%9F%A5%E8%AF%A2%E7%BB%93%E6%9E%9C/123%E6%B1%87%E6%80%BB.fa)中。~~
整理了 _仓库_  :添加了几个文件夹  

~~**待进行的任务** : 从文章中摘取他人已经鉴定好的NLP序列，并放进卵菌参考序列中。~~


## 绘制进化树
~~用上一步得到的blastp结果，同鉴定的PvNLP序列进行多序列比对，并绘制NJ系统发育树。使用[**evolview**](https://www.evolgenius.info/evolview/#mytrees/EXAMPLES/Sample%20tree%201(Simple%20tree%20example))
进行系统发育树的美化。将亲缘关系较近的leaf collapsed。
大豆疫霉，采用四个序列作为query进行blastp比对，取identify>=50%的序列，evalue小于1e-5的序列，并人工筛选在100aa到300aa的序列，并删除不完整序列，重命名。
![系统发育树](https://github.com/roywhite98/Atlanta/blob/dev/%E7%B3%BB%E7%BB%9F%E5%8F%91%E8%82%B2%E6%A0%91.png)~~

OK,之前做的就算是白做啦。
我们重新绘制系统发育树。并通过系统发育树预测PvNLP蛋白的功能性。使用[Comparative and Functional Analysis of the Widely Occurring Family of Nep1-Like Proteins](https://apsjournals.apsnet.org/doi/suppl/10.1094/MPMI-04-14-0118-R)这个dalao的文章中的数据，基于533个来自真菌，细菌，卵菌三个界，与已经鉴定的7个PvNLP蛋白绘制系统发育树。通过序列在该树中的离散情况，判定其对应功能。

