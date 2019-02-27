# ZeromapsFS API
## Cluster
### 获取cluster容量
请求方式：GET

请求路径：/admin/cluster/cap

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：


| 响应参数 | 类型 | 参数说明 | 是否必选 | 备注 |
| ----------- | ------------ | ------------ | ------------ | ------------ |
| total_disk_cap | string | 整个系统硬件总容量 | 是 | uint64 |
|total_disk_usage | string | 整个系统硬件的已用容量 | 是 | uint64 |

响应示例：
```python
{
	" total_disk_cap": "5461256461" ,
	" total_disk_usage": "4561646"
}

```
### 数据池性能监控
请求方式：GET

请求路径：/admin/cluster/perf

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：

| 响应参数  | 类型  |  参数说明 | 是否必选  |  备注 |
| ------------ | ------------ | ------------ | ------------ | ------------ |
| id  | string  | 数据池ID  |  是 |   |
| max_perf  | string  | 数据池最大QPS数  | 是  |   |
| ave_perf  |  string | 数据池平均QPS数   | 是  |   |
| min_perf  | string  |  数据池最小QPS数 | 是  |   |

响应示例：
```python
{
  "data_pools": [
    {
      "id ": "datapool-1",
      "max_perf": [
        28916,
        30064,
        29742,
        29851,
        32490,
        30282,
        29121,
        31434,
        31000,
        31500,
        31400,
        31600
      ],
      "avg_perf": [
        17744,
        17722,
        16005,
        19771,
        20185,
        19377,
        21147,
        22387,
        22000,
        21350,
        20000,
        21600
      ],
      "min_perf": [
        10908,
        9948,
        8105,
        11248,
        8989,
        11816,
        12274,
        12111,
        12000,
        12500,
        12100,
        12100
      ]
    }
  ]
}

```
## Hosts
### 获取hosts列表
请求方式：GET

请求路径：/admin/hosts

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：

|响应参数 | 类型 | 参数说明|是否必选|备注|
| ----------- | ------------ | ------------ | ------------ | ------------ |
|name | string | 服务器名称|是 | |
|start_time | string | 服务器开始启动时间|是|Uint64|
|cpu_usage | string | 服务器CPU利用率|是|float|
|memory_usage |string|服务器内存 |  是 | uint64|
|status | int | 服务器状态 | 是 |1, 0|

响应示例：
```python
{
  "hosts": [
    {
      "name": "stone160.f3322.net",
      "start_time": "int64",
      "cpu_usage": "0.3",
      "memory_usage": "100000000",
      "status": 0(成功)，1(失败)
    }
  ]
}

```
## Disks
### 获取磁盘信息
请求方式：GET

请求路径：/admin/disks

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：

 | 响应参数  | 类型 | 参数说明 | 是否必选 | 备注 | 
 | ----------- | ------------ | ------------ | ------------ | ------------ |
 | server_name | string | 服务器名称 | 是 |  | 
 | uuid | string | 磁盘编号 | 是 |   |  
 | db_contain | string | 包含的DB () | 是 |  |
 | cap | string | 单个磁盘容量 | 是 | uint64 | 
 | usage | string | 单个磁盘已用容量 | 是 | uint64 | 

响应示例：
 ```python
{
  "disks": [
    {
      "server_name": "stone160.f3322.net",
      "uuid": "010102",
      "db_contain": "包含的DB",
      "cap": "4615654561",
      "usage": "26646615"
    }
  ]
}

```
## Datapools
### 获取数据池信息
请求方式：GET

请求路径：/admin/datapools

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：

| 响应参数  |  类型  | 参数说明  | 是否必选  | 备注  |
| ----------- | ------------ | ------------ | ------------ | ------------ |
| id   | string  | 数据池ID  | 是  |   | 
| type  | string  | 存储数据类型  | 是  |   | 
| max_longitude  | string  | 最大经度  | 是  | ±135.7  | 
| min_ longitude  | string  | 最小经度  | 是  | ±20.7  | 
| max_latitude  | string  | 最大纬度  | 是  | ±68.3  | 
| min_latitude   | string  | 最小纬度  | 是  | ±30.3  | 
| amount  | string  | 数据池数据量  | 是  | uint64  | 
| google_earth_amount  | string  | 谷歌数据量  | 是  | uint64  | 

响应示例：
```python
{
  "datapools": [
    {
      "id": "datapool_id",
      "type": "datapool_Type",
      "max_longitude": "135.7",
      "min_ longitude": "-20.7",
      "max_latitude": "68.3",
      "min_latitude": "-30.3",
      "amount": "15462131",
      "Google_Earth_amount": "Google_Earth_amount"
    }
  ]
}

```
### 新建数据池
请求方式：POST

请求路径：/admin/datapools

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

请求数据：

 | 请求参数 | 类型 | 参数说明 | 是否必选 | 备注 | 
 | ----------- | ------------ | ------------ | ------------ | ------------ |
 | name | string | 数据池名称 | 是 |  | 
 | type | string | 数据类型 | 是 |  | 
 | max_longitude | float | 最大经度 | 是 | ±164.8 | 
 | min_ longitude | float | 最小经度 | 是 | ±32.7 | 
 | max_latitude | float | 最大纬度 | 是 | ±68.9 | 
 | min_latitude | float | 最小纬度 | 是 | ±31.2 | 

请求示例：
```python
{
  "datapool": {
      "name": "datapool_name",
      "type": "datapool_type",
      "max_longitude": "135.7",
      "min_ longitude": "-20.7",
      "max_latitude": "68.3",
      "min_latitude": "-30.3"
    }
}

```
## 公共Service
### 获取区域数据所占用的存储空间
请求方式：POST

请求路径：/commserv/calc_cap

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

请求数据：

 | 请求参数 | 类型 | 参数说明 | 是否必选 | 备注 | 
 | ----------- | ------------ | ------------ | ------------ | ------------ |
 | max_longitude | float | 最大经度 | 是 | ±164.8 | 
 | min_ longitude | float | 最小经度 | 是 | ±32.7 | 
 | max_latitude | float | 最大纬度 | 是 | ±68.9 | 
 | min_latitude | float | 最小纬度 | 是 | ±31.2 | 
 | type | string | 数据类型 | 是 |   | |

请求示例：
```python
{
    "max_longitude": "135.7",
    "min_ longitude": "-20.7",
    "max_latitude": "68.3",
    "min_latitude": "-30.3",
    "type": "datapool_type"
}

```
响应数据：

 | 响应参数 | 类型 | 参数说明 | 是否必选 | 备注 | 
 | ----------- | ------------ | ------------ | ------------ | ------------ |
 | cap | float | 最大经度 | 是 |    |
 | uuid | float | 最小经度 | 是 |    || 
 
响应示例：
```python
{
     "commserv": [{
          "cap": "486516",
          "uuid": "dasd"
      }, {
          "cap": "486516",
          "uuid": "dasx"
      }]
}

```