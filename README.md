# Mô tả API LBASense

##Thống kê chung

###Thống kê theo ngày
Đầu vào: 
  - region
  - date
  
```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&region=1&date=2016-09-26
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
  - region
  - hour

```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&region=1&hour=2016-09-26T16
```

Trả về 

```
{"summaryStats":[{"date":"2016-09-26T16:00:00","numVisitors":3001,"numReturningVisitors":2314,"avgDuration":1308}]}
```

Ý nghĩa: Lấy số liệu thống kê trong khoảng thời gian 1 tiếng từ 15h-16h 2016-09-26. Các tham số trả về tương tự như thống kê theo ngày.

###Thống kê theo khoảng thời gian
Đầu vào: 
  - region
  - startTime
  - endTime
  - resolution = [days/hours]
```
https://api.analytics.lbasense.com/StatsSummary?user=client123&pass=12345&region=1&startTime=2016-09-12T00:00:00&endTime=2016-09-26T02:00:00&resolution=hours&siteId=368
```
Trả về:

```
{"summaryStats":[{"date":"2016-09-26T00:00:00","numVisitors":183,"numReturningVisitors":135,"avgDuration":3800},{"date":"2016-09-26T01:00:00","numVisitors":86,"numReturningVisitors":67,"avgDuration":7983}]}
```

Ý nghĩa: Lấy số liệu thống kê theo giờ trong khoảng thời gian 2 tiếng từ 0h-2h ngày 2016-09-26. Các tham số trả về tương tự như thống kê theo ngày.

##Thống kê số lượng khách tới region theo "khoảng thời gian khách ở lại" của một hoặc một chuỗi ngày chỉ định.
Đầu vào: 
  - region
  - startTime
  - endTime
  
```
https://api.analytics.lbasense.com/VisitDurations?user=client123&pass=12345&region=1&startTime=2016-09-26&endTime=2016-09-30&siteId=368
```

Trả về

```
{"visitDurations":[{"date":"2016-09-26",
"under1Minute":17095,"from1To5Minutes":2594,"from5To10Minutes":1063,"from10To20Minutes":1265,"from20To40Minutes":1266,"from40To60Minutes":450,"from60To90Minutes":370,"from90To120Minutes":235,"from2To3Hours":205,"from3To4Hours":115,"from4To6Hours":72,"over6Hours":101},{"date":"2016-09-27",
"under1Minute":18228,"from1To5Minutes":2956,"from5To10Minutes":1267,"from10To20Minutes":1497,"from20To40Minutes":1543,"from40To60Minutes":657,"from60To90Minutes":561,"from90To120Minutes":340,"from2To3Hours":429,"from3To4Hours":167,"from4To6Hours":170,"over6Hours":154},{"date":"2016-09-28",
"under1Minute":18093,"from1To5Minutes":2959,"from5To10Minutes":1309,"from10To20Minutes":1507,"from20To40Minutes":1590,"from40To60Minutes":666,"from60To90Minutes":531,"from90To120Minutes":377,"from2To3Hours":396,"from3To4Hours":167,"from4To6Hours":166,"over6Hours":137},{"date":"2016-09-29",
"under1Minute":18082,"from1To5Minutes":2737,"from5To10Minutes":1302,"from10To20Minutes":1521,"from20To40Minutes":1514,"from40To60Minutes":602,"from60To90Minutes":561,"from90To120Minutes":319,"from2To3Hours":384,"from3To4Hours":180,"from4To6Hours":183,"over6Hours":139}]}
```

Ý nghĩa: Lấy số liệu trong thời gian 4 ngày từ 26 -> 30/9. THống kê xem trong mỗi ngày, có bao nhiêu người dành thời gian dưới 1 phút, từ 1 tới 5 phút, 5 tới 10 phút, ... trên 6 giờ, đứng tại khu vực có "region=1"

##THống kê số lượng khách tới region theo giờ hoặc theo ngày.
Ví dụ 1:
Đầu vào:
  - region
  - startTime
  - endTime
  - resolution = [days/hours]

```
https://api.analytics.lbasense.com/VisitorCounts?user=client123&pass=12345&region=1&startTime=2016-10-01T15:00&endTime=2016-10-01T18:00&resolution=hours&siteId=368
```
Trả về

```
{"dates":["2016-10-01T15:00:00","2016-10-01T16:00:00","2016-10-01T17:00:00"],"visitorCounts":[1059,1095,1286]}
```

Ý nghĩa: Thống kê theo giờ số  lượng người thăm khu vực "region=1" trong khoảng thời gian 15h->16h 2016-10-01, 16h->17h 2016-10-01, 17h->18h 2016-10-01.

Ví dụ 2:
Đầu vào:
  - region
  - hoursBack
  
```
https://api.analytics.lbasense.com/VisitorCounts?user=client123&pass=12345&region=1&hoursBack=3
```
Trả về:

```
{"dates":["2016-10-04T02:00:00","2016-10-04T03:00:00","2016-10-04T04:00:00"],"visitorCounts":[176,158,198]}
```

Ý nghĩa: Lấy số lượng khách thăm khu vực "region=1" trong mỗi 1 giờ, thống kê trong 3 giờ trước thời điểm hiện tại.

Ví dụ 3:
Đầu vào:
  - region
  - daysBack
  
```
https://api.analytics.lbasense.com/VisitorCounts?user=client123&pass=12345&region=1&daysBack=3
```
Trả về:

```
{"dates":["2016-10-01T00:00:00","2016-10-02T00:00:00","2016-10-03T00:00:00"],"visitorCounts":[16845,21403,29687]}
```

Ý nghĩa: Lấy số lượng khách thăm khu vực "region=1" trong mỗi ngày, thống kê trong 3 ngày trước thời điểm hiện tại.

##THống kê số lượng khách quay trở lại region theo giờ hoặc theo ngày.

Giống như API "THống kê số lượng khách tới region theo giờ hoặc theo ngày.", ta thay đầu vào VisitorCounts thành ReturningVisitorCounts trên url.

Ví dụ:

```
https://api.analytics.lbasense.com/ReturningVisitorCounts?user=client123&pass=12345&region=1&daysBack=3
```

Trả về:

```
{"dates":["2016-10-01T00:00:00","2016-10-02T00:00:00","2016-10-03T00:00:00"],"returningVisitorCounts":[9673,11234,20472]}
```

Ý nghĩa: Trả về số lượng người thăm "region=1" trong 1 ngày mà cũng đã từng thăm "region=1" trong 4 tháng trở lại đây, thống kê trong 3 ngày trước thời điểm hiện tại.

##THống kê thời gian thăm trung bình (theo giây) của khách tại một region theo giờ hoặc ngày.

Đầu vào:
  - region
  - startTime
  - endTime
  - resolution = [days/hours]

```
https://api.analytics.lbasense.com/AverageVisitDurations?user=client123&pass=12345&region=1&startTime=2016-10-03T14:00:00&endTime=2016-10-03T17:00:00&resolution=hours
```

Trả về:

```
{"averageVisitDurations":[2194,1965,1629],"dates":["2016-10-03T14:00:00","2016-10-03T15:00:00","2016-10-03T16:00:00"]}
```

##THống kê số lượng khách thăm region vào ngày chỉ định, đồng thời thăm region vào 1 số ngày trước đó.
Ví dụ 1:

Đầu vào:
  - region
  - daysBack
  
```
https://api.analytics.lbasense.com/PreviousVisits?user=client123&pass=12345&region=1&date=2016-10-03&daysBack=3
```
Trả về:

```
{"dates":["2016-10-02","2016-10-01","2016-09-30"],"previousVisits":[3810,4884,8367]}
```
Ý nghĩa: Vào ngày 2016-10-03, có một số X người thăm "region=1", trong X người đó, có 3810 người đã tới region1 vào ngày 2016-10-02, có 4884 người đã tới region1 vào ngày 2016-10-01, có 8367 người đã tới region1 vào ngày 2016-09-30

Ví dụ 2:
Đầu vào:
  - region
  - date

```
https://api.analytics.lbasense.com/DaysPresent?user=client123&pass=123455&region=1&date=2016-10-02
```

Trả về:

```
{"numPresent1Day":3375,"numPresent2Days":1801,"numPresent3Days":1148,"numPresent4Days":952,"numPresent5Days":768,"numPresent6Days":576,"numPresentAll7Days":388}
```

Ý nghĩa: Vào ngày 2016-10-02 có một số lượng X người thăm "region=1", trong X người đó, có 3375 người tới region1 trong 1 ngày của tuần trước đó, 1801 người tới region1 trong 2 ngày của tuần trước đó, ..., 388 cả tuần trước đó ngày nào cũng tới region1. 
