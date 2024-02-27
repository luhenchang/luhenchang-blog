# PostgreSql+Postgis空间函数

## 1.基础属性

### 1.WKT

WKT(Well-known text)是一种文本标记语言，用于表示矢量几何对象、空间参照系统及空间参照系统之间的转换。它的二进制表示方式，亦即WKB(well-known-binary)则胜于在传输和在数据库中存储相同的信息。该格式由开放地理空间联盟(OGC)制定。WKT可以表示的几何对象包括：点，线，多边形，TIN（不规则三角网）及多面体。以下为几何WKT字串样例：

```
POINT(6 10)//点
LINESTRING(3 4,10 50,20 25)//线
POLYGON((1 1,5 1,5 5,1 5,1 1),(2 2,2 3,3 3,3 2,2 2))//多边形
```

### 2.Geometry

 geometry为Arcgis中的几何对象，包括Extent、Multipoint、Point 、Polygon 、Polyline。

### 3.SRID（空间引用标识符）

 空间参考标识符 (SRID) 是与特定坐标系、容差和分辨率关联的唯一标识符，最常用的如下：

1. EPSG:4326 (WGS84)  ---GPS是基于WGS84坐标系 

2. EPSG:4490 (CGCS2000 2000国家大地坐标系)

3. EPSG:3857 (墨卡托投影坐标系)

## 2.引申概念 

#### 1.1、Geography数据类型是什么？Geography数据类型和Geometry数据类型区别又是什么？

PostGIS的GEOGRAPHY数据类型基于大地坐标系对经纬度坐标（也可称为大地坐标或者地理坐标）数据提供支持，大地坐标是用角度单位表示的球面坐标。而Geometry是基于二维笛卡尔坐标系-Cartesian Coordinate System（平面坐标系，投影坐标系）的，投影坐标通常是以米（meter）、千米（kilometer）等作为单位。

Geometry和Geography这两种数据类型的最大不同之处是它们对空间数据的计算方式不同，这也是最能体现Geography数据类型价值的地方。例如，计算两个坐标点的距离，Geometry数据类型的数据是基于平面坐标系来计算的，也就是将两个坐标点看作是处于同一个平面，使用类似勾股定理之类的公式，计算它们之间的平面距离。而Geography数据类型的数据是基于球面坐标来计算的，也就是将两个坐标点看作地球参考椭球体上的两个坐标点，计算它们之间的大圆航线的距离。

#### 1.2、Geography数据类型和空间

函数我们都知道，在球面上的计算比在平面上的计算更复杂，代价更高，所以Geography数据类型支持的空间函数比Geometry数据类型支持的空间函数少（PostGIS依赖的GEOS库实现的函数，没有一个支持Geography数据类型）。不过，Geography数据类型与Geometry数据类型可以相互转换。

## 3.注意事项

### 1.Postgresql的自增序列

 Postgresql的自增与MySQL的不同需要自己创建自增序列,具体方式如下：

```sql
-- 创建自增序列（表名+id+seq）
CREATE SEQUENCE tablename_id_seq
INCREMENT 1
MINVALUE  1
MAXVALUE 999999999
START 1
CACHE 1;
-- 设置对应表id默认值（直接粘贴到id的默认值中）
nextval('tablename_id_seq'::regclass)
-- 查看当前自增序列数值
SELECT * FROM  tablename_id_seq
-- 重置自增id为1ALTER SEQUENCE tablename_id_seq restart with 1;
-- 清除自增序列
DROP SEQUENCE tablename_id_seq
```

![image-20240227092531057](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240227092531057.png)

### 2.扩展添加

postgis是Postgresql中的一个扩展项，当数据库中没有geometry字段时，查看是否安装postgis扩展，完成安装后在对应表中执行以下语句

```sql
CREATE EXTENSION postgis;
```

### 3.SQL写法区别

```sql
-- 1、分页查询

例如查询0到10条数据
Postgresql select *from table limit 10 offset 0;
MySQL select *from table limit 0,10;
```

### **4.空间函数**

**常用函数：**

```sql
将空间数据（geom类型）以文本形式显示 ST_AsText(geom)
将wkt格式的文本数据转换为空间数据（geom类型） ST_GeometryFromText(text,SRID)
给空间数据设置坐标系id ST_SetSRID(geometry, integer)
坐标转换函数 ST_Transform(geom,SRID)
返回两个几何对象的距离（笛卡尔） ST_Distance(geometry, geometry)
判断两个几何对象是否在某一个范围内（单位：米） ST_DWithin(geometryA,geometryB,double b)
获取缓冲后的几何对象（单位：米） ST_Buffer(geometry, double)
判断A是否包含B ST_Contains(geometry A, geometry B)
根据经度和纬度返回空间数据 ST_Point(x y)
数据分割函数（需分割的数据，minX、maxX经度最大，最小值,分割份数）
width_bucket(st_x(geom), #{minX}, #{maxX}, 19)
获取几何对象的中心 ST_Centroid(geometry)
获取geom集合，通常和group by结合使用 ST_Collect(geometry)
获取数据集合 array_agg(id)
```

**管理函数：**

```sql
添加几何字段 AddGeometryColumn(, , , , , )
删除几何字段 DropGeometryColumn(, , )
检查数据库几何字段并在geometry_columns中归档 Probe_Geometry_Columns()
给几何对象设置空间参考（在通过一个范围做空间查询时常用） ST_SetSRID(geometry, integer)
```

**几何对象处理函数：**

![image-20240227100121603](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240227100121603.png)

**几何对象存取函数**

![image-20240227100040652](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240227100040652.png)

**几何量测函数**

```sql
量测面积 ST_Area(geometry)
根据经纬度点计算在地球曲面上的距离，单位米，地球半径取值6370986米
ST_distance_sphere(point, point)
类似上，使用指定的地球椭球参数 ST_distance_spheroid(point, point, spheroid) 量测2D对象长度 ST_length2d(geometry)
量测3D对象长度 ST_length3d(geometry)
根据经纬度对象计算在地球曲面上的长度 ST_length_spheroid(geometry,spheroid)
ST_length3d_spheroid(geometry,spheroid)
量测两个对象间距离 ST_distance(geometry, geometry)
量测两条线之间的最大距离 ST_max_distance(linestring,linestring)
量测2D对象的周长 ST_perimeter(geometry)
ST_perimeter2d(geometry)
量测3D对象的周长 ST_perimeter3d(geometry)
量测两点构成的方位角，单位弧度 ST_azimuth(geometry, geometry)
```

**几何对象编辑**

```
给几何对象添加一个边界，会使查询速度加快 ST_AddBBOX(geometry)
删除几何对象的边界 ST_DropBBOX(geometry)
添加、删除、设置点 ST_AddPoint(linestring, point, [])
ST_RemovePoint(linestring, offset)
ST_SetPoint(linestring, N, point)
几何对象类型转换 ST_Force_collection(geometry)
ST_Force_2d(geometry)
ST_Force_3dz(geometry), ST_Force_3d(geometry),
ST_Force_3dm(geometry)
ST_Force_4d(geometry)
ST_Multi(geometry)
将几何对象转化到指定空间参考 ST_Transform(geometry,integer)
对3D几何对象作仿射变化 ST_Affine(geometry, float8, float8, float8, float8,
float8, float8, float8, float8, float8, float8, float8, float8)
对2D几何对象作仿射变化 ST_Affine(geometry, float8, float8, float8, float8,
float8, float8)
对几何对象作偏移 ST_Translate(geometry, float8, float8, float8)
对几何对象作缩放 ST_Scale(geometry, float8, float8, float8)
对3D几何对象作旋转 ST_RotateZ(geometry, float8)
ST_RotateX(geometry, float8)
ST_RotateY(geometry, float8)
对2D对象作偏移和缩放 ST_TransScale(geometry, float8, float8, float8, float8) 反转 ST_Reverse(geometry)
转化到右手定则 ST_ForceRHR(geometry)
参考IsSimple函数
使用Douglas-Peuker算法 ST_Simplify(geometry, tolerance)
ST_SimplifyPreserveTopology(geometry, tolerance)
讲几何对象顶点捕捉到网格 ST_SnapToGrid(geometry, originX, originY, sizeX, sizeY) ST_SnapToGrid(geometry, sizeX, sizeY), ST_SnapToGrid(geometry, size)
第二个参数为点，指定原点坐标 ST_SnapToGrid(geometry, geometry, sizeX, sizeY,
sizeZ, sizeM)
分段 ST_Segmentize(geometry, maxlength)
合并为线 ST_LineMerge(geometry)
```

## **示例SQL**

**1.点位聚合**

```sql
SELECT
-- minx、maxx当前屏幕经度最大、最小值
-- minY、maxy当前屏幕纬度最大、最小值
-- 计算聚合后的点在屏幕分为16*9网格后在哪个网格
width_bucket(st_x(geom),minx, maxx, 19)grid_x,
width_bucket(st_y(geom),minY, maxY, 6)grid_y,
--聚合点包含点位数量
count(*)，
--合点包含哪些id(随机点位使用此id集合随机取点)
array_agg(id) ids,
from bs.ads_device_channel_info
WHERE
st_x(geom)between #{minx}and#{maxX}
and
st_y(geom)between #{minY} and #{maxY}
and
id is not nu17GRoUP BY grid_x, grid_y
```

![image-20240227095845484](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240227095845484.png)

![image-20240227095810775](/Users/wangfeiwangfei/Library/Application Support/typora-user-images/image-20240227095810775.png)