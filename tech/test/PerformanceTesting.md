# Web服务器性能测试
------
性能测试的目的，简单说其实就是为了获取待测系统的响应时间、吞吐量、稳定性、容量等信息, 而发现一些具体的性能相关的缺陷（如内存溢出、并发处理等问题），从更高的层次来说，性能测试最想发现的，是瓶颈。如何能得到所需要的信息，就需要从多方面进行测试

> * 基准测试
> * 压力测试


## 基准测试 
指通过设计科学的测试方法、测试工具和测试系统，实现对一类测试对象的某项性能指标进行定量的和可对比的测试。例如指定某个URL资源响应不能超过0.5秒或1秒.
## 压力测试 
指测试网站在某个特定的持续的访问压力下运行的稳定性(压力测试)，以及可以网站瞬间能承受的压力(负载或并发测试)。
### 例如
> * 同一时间100个用户连续3, 5, 20分钟访问网站，网站的打开时间受到多大影响
> * 同一时间用户并发访问的数量100, 300, 1000, 5000逐次增加

## 常用压力测试用具:
> *  ab - [Apache benchmarking tool](http://httpd.apache.org/docs/2.2/programs/ab.html)
> *  webbench - [官网](http://home.tiscali.cz/~cz210552/webbench.html)
它是由Lionbridge公司开发的知名的非常简单的网站压力测试工具, Webbench最多可以模拟3万个并发连接去测试网站的负载能力
> *  Apache JMeter - http://jmeter.apache.org/


### ab 测试
ab -n 1000 -c 100 http://www.zeniu.com/info.php
> * -n后面的1000代表总共发出1000个请求
> * -c后面的100表示采用100个并发（模拟100个人同时访问）
> * 后面的网址表示测试的目标URL。

#### 事例
> 
<pre>
[root@localhost apache2]# ./bin/ab -n 1000 -c 100 http://www.zeniu.com/info.php    
This is ApacheBench, Version 2.3 <$Revision: 1638069 $>    
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/   
Licensed to The Apache Software Foundation, http://www.apache.org/   
</pre>

<pre>
Benchmarking www.zeniu.com (be patient)
Completed 100 requests
Completed 200 requests
Completed 300 requests
Completed 400 requests
Completed 500 requests
Completed 600 requests
Completed 700 requests
Completed 800 requests
Completed 900 requests
Completed 1000 requests
Finished 1000 requests
</pre>

<pre>
Server Software:        Apache/2.4.12
Server Hostname:        www.zeniu.com
Server Port:            80
</pre>

<pre>
Document Path:          /info.php
Document Length:        76971 bytes
</pre>

<pre>
Concurrency Level:      100
Time taken for tests:   1.417 seconds
Complete requests:      1000
Failed requests:        98
   (Connect: 0, Receive: 0, Length: 98, Exceptions: 0)
Total transferred:      77184889 bytes
HTML transferred:       76970889 bytes
Requests per second:    705.52 [#/sec] (mean)
Time per request:       141.740 [ms] (mean)
Time per request:       1.417 [ms] (mean, across all concurrent requests)
Transfer rate:          53178.82 [Kbytes/sec] received
</pre>

<pre>
Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        4   72  36.7     74     149
Processing:     6   69  36.3     68     155
Waiting:        1   63  37.3     61     146
Total:        132  141   8.4    138     169
</pre>

<pre>
Percentage of the requests served within a certain time (ms)
  50%    138
  66%    140
  75%    141
  80%    143
  90%    160
  95%    161
  98%    169
  99%    169
 100%    169 (longest request)
</pre>


### webbench 测试
webbench -c 100 -t 20 http://www.zeniu.com/info.php
> -c是并发数 -t是运行测试时间，即20秒钟内中以每次100个请求进行测试

<pre>
[root@localhost webbench-1.5]# webbench -c 4000 -t 30 http://www.zeniu.com/info.php
Webbench - Simple Web Benchmark 1.5
Copyright (c) Radim Kolar 1997-2004, GPL Open Source Software.
</pre>

<pre>
Benchmarking: GET http://www.zeniu.com/info.php
4000 clients, running 30 sec.
</pre>

<pre>
Speed=69940 pages/min, -53046599 bytes/sec.
Requests: 34958 susceed, 12 failed.
</pre>

