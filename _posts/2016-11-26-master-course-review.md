---
layout: post
title: "NUS Master in Information System course review course review"
date: 2016-11-26 18:52:00 +0800
categories: others
---
[star]: /static/img/star-icon.png

# NUS Master in Information System course review

历时两年，经历了n个在学校刷project的夜晚，我的NUS master读书生涯终于要告一段落啦！总共分4学期完成10门课，特来做个course review 附个人评分（满分5颗星），以作纪念。

<br>

### 2014 - 2015 Sem2

第一学期我一口气选了3门IS的课，于是开启了一学期不停读论文写report模式，然后发现我真的不适合读文科！

* IS5110 SOFTWARE PROJECT MANAGEMENT

当初选择了IS而不是CS，一个原因是看到了这门课的存在。Project management,由码农升华为管理者是多么的高大上!

然而我还是太幼稚T_T。这门课的prof在学校教书三十年，所有教的都来自于各种论文而非任何亲身实践经验，不少东西也有些过时。上课基本上是一节课两个小组上台讲paper，然后两个人做individual presentation分享个人经验，而老师基本只做最后的总结评论。

有一个group project，要求自己找paper关于cost/time之类estimation，然后写类似literature review的report。为了这个Project当初找了好多report,现在唯一的印象就是里面各种完全看不懂数学公式来算cost estimation，不知道实际工作中还有多少项目是这样做估计的。

难度   ![star][star]

Project难度   ![star][star] ![star][star] ![star][star]

实用性 ![star][star] ![star][star]


* IS5114 INFORMATION TECHNOLOGY OUTSOURCING

这门课讲了各种形式的外包和外包过程中可能产生的问题。老师是NTUC的CIO，上课她会给很多她与外包（咨询）公司打交道的例子，还算IS里面比较有用的一门课。可是它为什么不是Core！

Assignment是做一个outsourcing的case study。当时我的组做了一个外包失败的case study，老师表示很喜欢。
有期末考，老师会在考试前做一个dry run让大家熟悉题目类型了解打分要求，所以期末难度不大。

难度 ![star][star] ![star][star]

Project难度   ![star][star] ![star][star] 

实用性 ![star][star] ![star][star] ![star][star]

* IS5117 ELECTRONIC GOVERNMENT

这门课讲IT在government中的应用，印象比较深的是关于G-cloud，因为之前听说了太多关于它的吐槽（compare to AWS）。老师也是adjunct prof，一般他讲半节课，另外半节课请外面的人来讲。

Assignment一组7个人写6页纸的report...于是最后一直在努力的缩减长度，然后组里选两个人上去做presentation。期末考试是非常传统的文科考试形式，各种写小短文。

听说现在这门课换了老师于是变得完全不一样了。

难度 ![star][star]

Project难度 ![star][star]

实用性 ![star][star] 

<br>

### 2015 - 2016 Sem1

由于是新的学年，课表有不小改动，很多之前在下学期开的课移到了上学期，于是这一学期很多课程和之前的学期重复可选课很少。

* CS5226 DATABASE TUNING

这门课讲了各种database tuning的方法，比如query tuning, lock tuning。老师是澳大利亚某大学的老师过来客串一学期，但他毕业于哈工大。。。每节课他讲一小时然后放一小时的youtube，大家笑称每节课花上百的tuition fee来看youtube。

这门课内容有用但缺乏实践。Assignment是写report，要求和FYP类似，manual说是要让大家练习写论文能力。当时我苦思冥想好久决定做了个MS SQL Server和Oracle的对比，最后report得到了老师的肯定哈哈。

选课的时候以为这门课没有期末考，后来才知道是老师不懂需要向学校申请有期末考试，于是最后随堂考完了期末。

难度 ![star][star] ![star][star] ![star][star] 

Project难度 ![star][star] ![star][star] ![star][star] ![star][star]  （难度给我当年真的花了好久想research主题）

实用性 ![star][star] ![star][star] ![star][star]

* IS5151 INFORMATION SECURITY POLICIES

读这门课的时候在银行做项目，每天特别烦电脑没有admin access，每次装任何东西都要找admin来帮忙。学这门课自己写了改了不少security policy，感觉能理解一些制定这些policy的人的难处了。

嗯，这门课就是关于如何制定公司里面的information security policy。如果能拿到自己公司的security policy仔细读读各项条款大概就能明白一二了。当时自己组队的队友们全部都是读information security的，于是我华丽丽的打了个酱油。

听说之前这门课特别难，但我这学期换老师了老师给分还不错。

难度 ![star][star] ![star][star] ![star][star]

Project难度 ![star][star] ![star][star] ![star][star]

实用性 ![star][star] ![star][star] ![star][star]

<br>

### 2015 - 2016 Sem 2

* CS5331 WEB SECURITY
在两学期之间的那个假期里，我被派去做个Penetration testing 的项目，于是新学期便选了这门课来系统学习一下。

这门课讲了各种形式的fraud，比如xss, sql injection，但都比较基础。

Assignment分4个，每组4个人。前三个都近乎Individual assignment。
第一个可以忽略，第二个是让给某个PHP开源project加新的function，和security并没有什么关系只是让大家熟悉Php。为什么是PHP呢，因为它漏洞多。。。默默的同情下PHP，有点哀其不幸怒其不争的feel。
第三个给了32个网页，要求按类别找漏洞并提交相应的攻击代码，每个小组成员找8个。
最后一个作业比较大，是选择一个attack类别写个auto detect漏洞的程序。程序分4步：1. 爬虫找到所有页面 2. 准备测试attack的代码 3. 结合前两步找到所有可疑的漏洞 4. 通过automation test证明漏洞的存在。
为了这个作业连续一周每天下班以后去学校写代码到凌晨2点回家再写1个小时，想起来都是泪T_T，每次熬夜的时候都在想自己为什么要读master...还好最后给分还不错...
 
 难度 ![star][star] ![star][star] ![star][star]
 
 Project难度 ![star][star] ![star][star] ![star][star] ![star][star] ![star][star]
 
 实用性 ![star][star] ![star][star] ![star][star] ![star][star]

* IS5128 ORGANIZING FOR IT INNOVATION

这门课是关于如何让公司变得Innovative，比如采取crowd sourcing集思广益之类的。
老师基本从头到尾都没讲过话的一门课，总共读了30篇paper，10个组每节课轮流上去讲，每个组半小时。

Assignment是找个公司做case study，从几个方面分析公司能如何变得更Innovative，不过这种东西只有做到公司高层才有可能去实践吧。此Assignment依旧包括presentation。
作业还包括2个case study，想当年第一个case study下来的时候正好春节，于是大过年的在家写作业T_T

 难度 ![star][star] ![star][star]
 
 Project难度 ![star][star] ![star][star] ![star][star] ![star][star]
 
 实用性 ![star][star] ![star][star]
 
* IS5152 DECISION MAKING TECHNOLOGIES

纯数学的一门课，包含了machine learning里面需要用到的各种数学，各种公式算法。
作为一个数学不好的人，我为什么要选这门课？因为当初选课的时候经常一起刷课的小伙伴说project三缺一来不来！

这门课虽然在IS名下，但只给了SOC学生10个名额，所以还是挤破头才选上的一门课。读这门课的其他人都是学数学之类的出生。于是最后自己期末考被虐的很惨，拿到了有史以来（包括大学）的最低分！

（PS：这门课也属于biz于是每次晚上的课都有buffet吃）

 难度 ![star][star] ![star][star] ![star][star] ![star][star] （纯属自己数学基础不好上课完全听天书）
 
 Project难度 ![star][star] ![star][star] ![star][star] 
 
 实用性 ![star][star] ![star][star] ![star][star]
 
<br>

### 2016 - 2017 Sem1

* IS5127 MANAGING AND USING NEW MEDIA

终于迎来了最后一学期，还差两门课其中一门需要是core。IS5127是唯一能选的Core非选不可，因为这个我都打算skip掉这学期下学期再毕业。

这门课是有名的水，主要原因之一是老师。这老师有多不靠谱呢，一学期13节课他临时取消了3节，两次是自己病了一次是前几天电脑坏了于是没有准备lecture slides。
之前这门课只有一个40页report加期末presentation，于是很多人都翘课不上。到了这学期老师突然改了风格，每节课随机考quiz逼大家出席，还加了一个和上课内容有关的individual assignment。
presentation被取消，40页的report还是要写。每周还会发出peer review的link，如果不填那周的平时成绩就拿不到了。。。

到最后这门课具体讲了啥我还是没有印象 o_O||

 难度 ![star][star] ![star][star] 
 
 Project难度 ![star][star] ![star][star] ![star][star] 
 
 实用性 ![star][star]

* CS4224 DISTRIBUTED DATABASES

备受好评的一门课，就是因为选上了这门课我放弃了自己延迟毕业的想法！内容很全面，包括distributed database query processing, indexing, concurrency control, data replication等等。

老师很认真，所有内容都有详细的例子图解，每节课还有相应的不算分的quiz帮助理解。提供lecture recording可以课（fang）后(bian)复(qiao)习(ke)。
Assignment任务相当重，需要用mongoDB和Cassandra两种DB做出一个wholesale supplier system，数据量几个G，每个组3个人会分到3个学校的node供测试用。
所幸另一门课比较水+队友给力（TWer的水平果然是值得信赖的），避免的通宵的悲剧。不过通过Assignment可以对这两个db有比较全面的理解。

Individual assignment和final都不算难（也许是因为课讲的很清楚），希望能拿到一个好分数！

 难度 ![star][star] ![star][star] ![star][star] 
 
 Project难度 ![star][star] ![star][star] ![star][star] ![star][star] ![star][star] 
 
 实用性 ![star][star] ![star][star] ![star][star] ![star][star] 
