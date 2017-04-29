---
title: About apache ab tools
date: 2017-04-29 19:30:22
tags:
---

服務器開發人員都會用併發數來談服務器的能力高低。其實他們很懶，隱藏了很多條件，就是

* 總量
* 時間
* 業務

依賴上述，能很好的計算出當前**服務器對於某個業務**來說是否勝任。而談能力高低似乎就沒有太大的意義，因為必須要置於一個業務範圍內考量才行。

[Throughput](https://en.wikipedia.org/wiki/Throughput)，吞吐量（吞吐率），就是由上面的參數計算出來的。可以通過apache的ab命令，結合上面的參數，配合不同的，對服務器承載業務進行一個測試，得出Throughput。

<!--More-->


## 業務

對於Web服務來說，業務可以抽象為妳的API endpoint。因為可以通過暴露API，來展示自己的業務。對於基於HTTP的API來說，每個URL就是妳的業務。

所以，業務這個參數，就可以理解為一條URL

## 時間與總量

時間無須解釋，總量就是在**一段時間**內，能做多少，兩者必須預先設定一個。

而時間與總量的關係，又可以如下描述

你現在有了自己的業務（URL），那麼你一定想知道你的業務員（服務器）在**一段時間內**能做些啥吧，比如

1. 一段時間內處理多少URL
2. 一個URL用了多少時間



## ApacheBench,ab

ab對上述的條件做了很好的組織，這樣就可以愉快的給業務員（服務器）壓力了。

```shell
root@vultr:~# ab -n1000 -c300 http://127.0.0.1/rating/dfx
```

設定了業務（URL）、requests（總量）和concurrency，ab就會給出時間和計算結果。

所以，在總量是1000，併發數300的情況下：（前提非常重要）

1. Requests per second:    322.72 [#/sec] (mean)  每秒處理請求數「平均」
2. Time per request:       929.602 [ms] (mean)  一個請求的用戶等待時間「平均」
3. Time per request:       3.099 [ms] (mean, across all concurrent requests)  全部請求的用戶等待時間「平均」



## 總結

上述的1可以理解為吞吐率，2可以理解為一個URL要用多少時間，3完成全部需要多少。

##### ab輸出的部分內容如下

```shell
Concurrency Level:      300
Time taken for tests:   3.099 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      178000 bytes
HTML transferred:       20000 bytes
Requests per second:    322.72 [#/sec] (mean)
Time per request:       929.602 [ms] (mean)
Time per request:       3.099 [ms] (mean, across all concurrent requests)
Transfer rate:          56.10 [Kbytes/sec] received
```

##### 完整output

```shell
This is ApacheBench, Version 2.3 <$Revision: 1706008 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 127.0.0.1 (be patient)
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


Server Software:        nginx/1.10.0
Server Hostname:        127.0.0.1
Server Port:            80

Document Path:          /rating/dfx
Document Length:        20 bytes

Concurrency Level:      300
Time taken for tests:   3.099 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      178000 bytes
HTML transferred:       20000 bytes
Requests per second:    322.72 [#/sec] (mean)
Time per request:       929.602 [ms] (mean)
Time per request:       3.099 [ms] (mean, across all concurrent requests)
Transfer rate:          56.10 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    7  11.1      0      29
Processing:    38  422 610.2    171    3036
Waiting:       34  422 610.2    171    3036
Total:         61  429 614.9    172    3060

Percentage of the requests served within a certain time (ms)
  50%    172
  66%    182
  75%    184
  80%    213
  90%   1687
  95%   1744
  98%   1776
  99%   3022
 100%   3060 (longest request)
```
