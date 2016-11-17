# 本次项目的负责人：吴腾跃

# 以下是项目环境，任务要求，实现方法，请认真查阅

1.环境搭建
  --Hadoop版本：本次项目使用Hadoop2.6.5，jdk1.8；
  --集 群 数 目：集群使用10台机器，1台作为master，其余作为slave；
  --机 器 配 置：机器最低配置4核2G内存100G硬盘； 
  
2.任务要求
  --使用陈老师提供的数据完成以下任务；
    每个任务均从hdfs中获取数据，并写到hdfs中的某某文件夹；
    所有数据均在hdfs的/home/hadoop/qst/ray中
      a.完成每天的UV统计
      b.完成每天访问量Top10的Show统计
      c.完成每天的次日留存统计

3.实现方法
  --a.
      1)通过map拿到所有IP，作为key值，以(IP, null)形式输出给reduce（UV可使用IP表示，即一个IP是一个UV；）；
      2)在reduce中，将IP放到Set集合中去重；
      3)Set大小即是UV数目，输出Set.size到文件中；
  
  --b.
      1)通过map拿到所有的show，每个show以(show, 1)的形式输出给reduce；
      2)reduce拿到(show, 1)，统计每个show的value的和；
      3)对value进行倒序排序，取出top10,输出到文件中；
  
  --c.
      1)统计当日的UV，生成(UV, 1),昨日的UV，生成(UV, 1)，数据合并;
      2)将两天的数据进行mapreduce，统计value值为2的UV，即为留存熟路；
      3）留存数目/昨日的UV数目，即是留存比例；
