# Mô tả API LBASense

##Thống kê chung

###Thống kê theo ngày
Đầu vào: 
  - populationType
  - region
  - date
  
```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&&populationType=0&region=1&date=2016-09-26
```

Trả về 

```
{"summaryStats":[{"date":"2016-09-26","numVisitors":27471,"numReturningVisitors":16915,"avgDuration":671}]}
```

Ý nghĩa: Lấy số liệu thống kê ngày 2016-09-26. Trong đó
  - numVisitors: Tổng số lượng người tới khu vực "region=1"
  - numReturningVisitors: Số lượng người quay trở lại khu vực "region=1" vào ngày 2016-09-26 trong khoảng 4 tháng gần đây.
  - avgDuration: Khảng thời gian trung bình tính theo giây mà mọi người đứng tại khu vực "region=1" vào ngày 2016-09-26
  
###Thống kê theo giờ
Đầu vào: 
  - populationType
  - region
  - hour

```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&&populationType=0&region=1&hour=2016-09-26T16
```

Trả về 

```
{"summaryStats":[{"date":"2016-09-26T16:00:00","numVisitors":3001,"numReturningVisitors":2314,"avgDuration":1308}]}
```

Ý nghĩa: Lấy số liệu thống kê trong khoảng thời gian 1 tiếng từ 15h-16h 2016-09-26. Các tham số trả về tương tự như thống kê theo ngày.

###Thống kê theo khoảng thời gian
Đầu vào: 
  - populationType
  - region
  - startTime
  - endTime
  - resolution = [days/hours]
```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&&populationType=0&region=1&startTime=2016-09-12T00:00:00&endTime=2016-09-26T02:00:00&resolution=hours&siteId=368
```
Trả về:

```
{"summaryStats":[{"date":"2016-09-26T00:00:00","numVisitors":183,"numReturningVisitors":135,"avgDuration":3800},{"date":"2016-09-26T01:00:00","numVisitors":86,"numReturningVisitors":67,"avgDuration":7983}]}
```

Ý nghĩa: Lấy số liệu thống kê theo giờ trong khoảng thời gian 2 tiếng từ 0h-2h ngày 2016-09-26.

