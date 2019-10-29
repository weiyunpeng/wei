### 距离函数

> 移动端附近的人，附近的地点功能十分常见,基于地理位置的服务（LBS）和相关应用也越来越多，而支撑这些应用的最基础技术之一，就是基于地理位置信息的处理。

- [mysql-st_distance](https://dev.mysql.com/doc/refman/5.6/en/spatial-relation-functions-mbr.html)

```sql
 st_distance 函数
 st_distance 函数是从mysql5.6.1才加入的。
 t_distance 计算的结果单位是度，需要乘111195（地球半径6371000*PI/180）是将值转化为米。
 SET @g1 = POINT(1,1), @g2 = POINT(2,2);
 select st_distance (@g1, @g2);
 输出结果：1.4142135623730951
```
#### 应用场景：
假设我当时的坐标：117.069,35.86 需要查询我附近50KM内服务区，并按照距离由近及远排列
```sql
SELECT 
s.id,s.name,s.lng,s.lat, 
(st_distance (point (lng, lat),point(117.069,35.86) ) *111195) AS distance 
FROM 
road_servicearea s 
HAVING distance<50 
ORDER BY distance
```