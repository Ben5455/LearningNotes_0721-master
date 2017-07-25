# 学习笔记0721
短短三天，吴秋生博士讲解了许多目前最热门的技术及其应用，就像是为我们打开了一扇又一扇的知识大门。俗话说工欲善其事必先利其器，这次吴博士就为我们带来了十八般兵器。但是欣喜之余，我也产生了两个困惑，一是好的工具这么多，时间精力却有限，我该如何选择哪些深入学习呢？二是有了这些工具我可以做什么？我该如何培养自己的思维，找到问题的研究切入点呢？在思考这两个问题之前，我决定先整理出三天课程的内容，既为复习巩固，也为日后回顾。
    
![课程表](https://github.com/Ben5455/LearningNotes_0721-master/blob/master/Image/classeslist.jpg)


## lidar
激光雷达的原理就是从地面或空中向地面发射激光，并获取其反射光束，通过反射激光的到达时间、强度和波长来获取地面的高程和其他信息。由于发射激光束十分密集，因此得到的激光点云数据空间分辨率（亚米级）能远远高于普通遥感系统（米或数十米级）。按照平台高度，lidar可分为空中（Airborne）激光雷达与地面（Terrestrial lidar）激光雷达；按照应用范围不同，可分为测陆激光雷达与测海激光雷达。后者使用蓝绿波段，在遇到水体时将被吸收而不产生反射光束，在图像上形成一片黑影易于与陆地区分。

激光点云数据的通用格式是.las格式，在ArcGIS存储格式是las dataset。与早期用户需要自己将激光点云数据一步步地转换成DEM不同，新版本的ArcGIS有相应的工具，用户只需要简单的点击鼠标，就能得到研究中常用的DEM。再加上现在的激光点云数据都带有丰富的属性和经过初步分类，因此用户可以自由选择显示哪些地物类型的点；第几次反射生成的点；生成包含所有地物高程的DHM或者是只保留地表的DEM……而最后一种往往是水文分析中不可或缺的。【图】激光点云数据中包含元数据，记录着数据制作日期、点云密度、天气状况等等。点云密度可以帮助用户设定输出恰当空间分辨率的DEM。激光点云数据自身是不带坐标系的，因此需要结合GPS的定位数据和测量平台的运动轨迹为数据赋予坐标。【图】从离散的点云数据插值到连续的地表面容易在不同地物类型的边界上产生误差，在ArcGIS中可以向加入辅助数据（如地物边界），使插值表面更准确。

借助Portable Basemap Server这款软件，能够把Google map和Bing map甚至是全球范围内一般精度的lidar数据导入到ArcGIS中作为底图显示，其优点是便捷，数据集全，且无需下载，随时调用。结合ArcGIS自带的Image Analysis，能在不下载数据的情况下，就实现对数据的空间分析，极大的节省了时间和存储空间。（这与下一节学习的GEE类似，不过后者更进一步将数据处理过程也交给云端完成，把本地计算机从繁重的运算中解脱了出来）如果对系统进行空间分析时的计算过程感兴趣，可以使用WhiteboxGAT软件，它不仅拥有大部分与lidar相关的空间分析功能，而且其中的代码都是可以随时查看的，名副其实的白箱子。这种大数据+云计算+开源的模式现在非常流行，具有很大的潜力。【图】(可是由于对软件不熟悉，和ArcGIS破解不完全的原因，PBS和IA目前都无法使用，后续会继续尝试修复)用于PBS的ArcGIS地图服务地址：http://imageryworkflows.ArcGIS.com:6080/ArcGIS /rest/services

## Google Earth Engine
Google earth engine简称GEE，是一个免费的在线地理信息获取、分析与展示平台。GEE的优点可以概括为地理数据获取容易、运算能力强大、空间分析算法灵活、实例代码齐全。数据无需下载，根据数据编码可直接调用；服务器端66000台电脑并行计算，运算能力远超单机时代；系统本身已封装了很多常用的空间分析方法，用户可以灵活调用组合，如果已有函数不满足需要，GEE支持用Javascript语言编写算法（同样支持python，但是配置python会麻烦许多）。使用GEE需要用户具备一定的编程基础，这让许多人望而却步，但是系统编写了大量的实例代码，帮助用户快速掌握系统的使用，而且一旦掌握了这项工具，对以后工作的效率会有极大的提升。
接下来尝试以提取广东地区的植被指数为例，介绍GEE的工作过程。



## git
Git实质是一个版本控制工具，适合用来追踪小型的，文本类型的，但具有多个版本的文件的编写过程。当用户用Git对一个文件夹进行管理时，Git会记录文件夹内所有变化，包括文件的增删、修改。用户可以随时设定文件夹当前状态为还原点，日后如果有需要，就能通过Git恢复到当前状态。
GitHub是一个使用Git工具进行项目管理的网站，人们在网站上可以协作完成项目，也可以任意创建/上传自己的项目或者拷贝别人的公开项目。如本次课堂笔记就是作为一个项目上传到了GitHub，任何人都可以进入我的项目列表中浏览。更进一步，GitHub为用户提供域名和服务器空间，允许用户建立个人网站，这无疑为用户展示自己项目成果提供了方便。


## R
在统计分析领域久闻R语言的大名，经过这次学习它复杂而又灵活的统计分析功能和图形展示功能令我印象深刻。R语言是免费开源项目，其源代码被托管在GitHub上，任何人都可以下载使用或者帮助维护。大部分的常用的函数都包含标准安装文件里，一些特定分析方法的函数可以随时通过载入在线的程序包获取（使用前需对程序包的代码有充分的了解），或者用户可以自行编程实现算法并共享到网络上。R语言适宜于用来处理文本文件，因此使用R语言时输入CSV文件比Excel文件更好。R语言处理文件时会将数据全部加载到内存中，处理完再新建文件存储。这样的好处是不会影响原文件，缺点是占用内存大。附上一个R语言搜索引擎，许多与R语言相关的问题都能从这里得到答案：http://rseek.org/

在ArcGIS中，用户无法对属性表数据进行复杂的统计分析，而R语言可以解决这个问题。要想中使用R语言分析空间数据，需要安装r-bridge组件。用户还可以用R语言开发工具集成到ArcGIS中以满足特定的需要。


