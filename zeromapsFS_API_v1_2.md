# Zeromaps-storage API
## 读写数据的数据类型
    ifile             //卫星影像数据
    tfile             //高程数据
    vector            //地名及路网数据
    q2                //卫星影像、高程、地名及路网数据的索引
    qp                //历史影像数据索引
    tmifile           //历史影像数据
    tile              //倾斜摄影二维数据
    bulkmetadata      //倾斜摄影数据的索引
    nodedata          //倾斜摄影数据
    
## 读写数据的方式
    gqtree            //tilekey方式读写
    tms               //OGC标准的TMS协议方式读写
    
## 写数据
请求方式: PUT

请求地址：http://{HOST}:{PORT}/store/{storetype}/{datatype}/{key}

请求示例1：http://127.0.0.1:8036/store/gqtree/ifile/0

请求示例2：http://127.0.0.1:8036/store/tms/ifile/1_1_1

参数说明：

|    参数     |      描述    |     备注    |
| ----------- | ------------ | ------------ |
|     PORT    |     端口号   |    默认8036   |
|   storetype |   读写方式   |  gqtree或tms  |
|   datatype  |   数据类型   |ifile,tfile,vector,q2,qp,tmifile.tilt,bulkmetadata,nodedata|
|      key    |     索引     | gqtree读写方式用tilekey,tms读写方式用x_y_z |

数据格式：二进制

数据说明：数据放在http请求的body中

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

## 读数据
请求方式: GET

请求地址：http://{HOST}:{PORT}/store/{storetype}/{datatype}/{key}

请求示例1：http://127.0.0.1:8036/store/gqtree/ifile/0

请求示例2：http://127.0.0.1:8036/store/tms/ifile/1_1_1

参数说明：

|    参数     |      描述    |     备注    |
| ----------- | ------------ | ------------ |
|     PORT    |     端口号   |    默认8036   |
|   storetype |   读写方式   |  gqtree或tms  |
|   datatype  |   数据类型   |ifile,tfile,vector,q2,qp,tmifile.tilt,bulkmetadata,nodedata|
|      key    |     索引     | gqtree读写方式用tilekey,tms读写方式用x_y_z |

响应的数据格式：jpg, jpeg, png

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |


# ZeromapsFS API
## 数据类型及其对应编号大小                                                                            
    IFile        uint32 = 1 //卫星影像数据类型                                 
    TFile        uint32 = 2 //高程数据类型                                     
    DFile        uint32 = 3 //地名及路网数据类型                               
    Q2           uint32 = 4 //卫星影像、高程、地名及路网数据的索引                 
    QP           uint32 = 5 //历史影像数据索引                             
    TMIFile      uint32 = 6 //历史影像数据                                 
    Tilt         uint32 = 7 // 倾斜摄影二维数据                                
    BulkMetaData uint32 = 8 //倾斜摄影数据索引                                 
    NodeData     uint32 = 9 //倾斜摄影数据                                     
   
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

| 响应参数 | 类型 | 参数说明 | 是否必选 | 备注|
| ----------- | ------------ |------------ |------------ |------------ |
| total_disk_cap | uint64 | 整个系统硬件总容量 | 是 | 返回字节数|
|total_disk_usage |uint64 | 整个系统硬件的已用容量 | 是 | 返回字节数|

响应示例：

```json
{
    "total_disk_cap": 5461256461 ,
    "total_disk_usage": 4561646
}

```
###  获取Cluster中各个类型数据的数据量
请求方式：GET

请求路径：/admin/cluster/typecaps

数据类型：application/json

响应码：

| Code | Reason |
| ----------- | ------------ |
| 200 - OK   | Request was successful  |

响应数据：

| 响应参数| 类型| 参数说明| 是否必选| 备注| 
| ----------- | ------------ |------------ |------------ |------------ |
| ifile_cap| uint64| 整个系统影像数据量| 是| 返回字节数| 
| tfile_cap| uint64| 整个系统高程数据量| 是| 返回字节数| 
| dfile_cap| uint64| 整个系统矢量和路网数据量| 是| 返回字节数| 
| tmifile_cap| uint64| 整个系统历史影像数据量| 是| 返回字节数| 
| strfile_cap| uint64| 整个系统街景数据量| 是| 返回字节数| 
| tilt_cap| uint64| 整个系统倾斜射影数据量| 是| 返回字节数| 
| photo_cap| uint64| 整个系统图片数据量| 是| 返回字节数| 

响应示例：
```json
{
    "dfile_cap": 8561246,
    "ifile_cap": 5461256461,
    "photo_cap": 34452461646,
    "strfile_cap": 289734561646,
    "tfile_cap": 4561646,
    "tilt_cap": 435642361646,
    "tmifile_cap": 12456314646
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

| 响应参数  | 类型  |  参数说明 | 是否必选  |备注|
| ------------ | ------------ | ------------ | ------------ |------------ |
| id  | string  | 数据池ID  |  是 | |
| max_perf  | uint64  | 数据池最大QPS数  | 是  | |
| ave_perf  | uint64 | 数据池平均QPS数   | 是  | |
| min_perf  | uint64  |  数据池最小QPS数 | 是  | |

响应示例：
```json
{
    "datapools": [
        {
            "id ": "d05h-fs93sfsui4g42",
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
| ----------- | ------------ | ----------- | ------------ |----------- | 
|name | string | 服务器名称|是 |  |
|start_time | string|服务器开始启动时间|是|时间戳 |
|cpu_num | uint32|服务器CPU核数|是| |
|cpu_usage | float64 | 服务器CPU利用率|是| |
|memory_info |string|服务器内存信息 |  是 |单位kB |
|status | int32 | 服务器状态 | 是 |1 工作, 0 宕机|

响应示例：
```json
{
    "hosts": [
        {
            "name": "stone160.f3322.net",
            "start_time": "1464242627",
            "cpu_num": 16,
            "cpu_usage": 0.3,
            "memory_info": {
                "total": "3423472674",
                "free": "2831241234",
                "available": "3134627356"
            },
            "status": 1
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

 | 响应参数  | 类型 | 参数说明 | 是否必选 |备注|
 | ----------- | ------------ |------------ |------------ |------------ |
 | server_name | string | 服务器名称 | 是 | |
 | uuid | string | 磁盘编号 | 是 | |
 | db_contain | int[ ] | 包含的DB () | 是 |1~9表示不用数据类型的DB|
 | cap | uint64 | 单个磁盘容量 | 是 | 返回字节数 |
 | usage | uint64 | 单个磁盘已用容量 | 是 | 返回字节数 |

响应示例：
```json
{
    "disks": [
        {
            "disk_infor": [
                {
                    "cap": 40000,
                    "db_contain": [
                        1
                    ],
                    "usage": 10000,
                    "uuid": "edf3342-g234t2g543f"
                },
                {
                    "cap": 40000,
                    "db_contain": [
                        4
                    ],
                    "usage": 10000,
                    "uuid": "010102"
                },
                {
                    "cap": 40000,
                    "db_contain": [
                        2,
                        3
                    ],
                    "usage": 10000,
                    "uuid": "010102"
                }
            ],
            "server_name": "stone160.f3322.net"
        },
        {
            "disk_infor": [
                {
                    "cap": 60000,
                    "db_contain": [
                        4,
                        1
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                },
                {
                    "cap": 60000,
                    "db_contain": [
                        2
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                },
                {
                    "cap": 60000,
                    "db_contain": [
                        3,
                        4
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                },
                {
                    "cap": 60000,
                    "db_contain": [
                        "i",
                        "t",
                        "d"
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                },
                {
                    "cap": 60000,
                    "db_contain": [
                        2
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                },
                {
                    "cap": 60000,
                    "db_contain": [
                        1
                    ],
                    "usage": 20000,
                    "uuid": "010104"
                }
            ],
            "server_name": "stone205.f3322.net"
        },
        {
            "disk_infor": [
                {
                    "cap": 50000,
                    "db_contain": null,
                    "usage": 5000,
                    "uuid": "010107"
                },
                {
                    "cap": 50000,
                    "db_contain": [
                        1,
                        3,
                        2
                    ],
                    "usage": 5000,
                    "uuid": "010107"
                },
                {
                    "cap": 545365,
                    "db_contain": [
                        5
                    ],
                    "usage": 5000,
                    "uuid": "010107"
                },
                {
                    "cap": 53423545,
                    "db_contain": [
                        2,
                        5
                    ],
                    "usage": 35657,
                    "uuid": "010107"
                }
            ],
            "server_name": "stone209.f3322.net"
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
| name | string  | 数据池名称 | 是  |   | 
| id   | string  | 数据池ID  | 是  |   | 
| type | uint32  | 存储数据类型  | 是  | 1-9代表各种数据类型  | 
| max_longitude  | float64  | 最大经度  | 是  | ±135.7  | 
| min_ longitude | float64  | 最小经度  | 是  | ±20.7  | 
| max_latitude  | float64  | 最大纬度  | 是  | ±68.3  | 
| min_latitude   | float64  | 最小纬度  | 是  | ±30.3  | 
| amount  | uint64  | 数据池数据量  | 是  | 存储数据量(条目数) | 
| size  | uint64  | 数据池已存储数据大小  | 是  | 存储数据大小(所占空间) | 
| google_earth_amount  | uint64  | 谷歌数据量  | 是  |  谷歌总量 ||

响应示例：
```json
{
    "datapools": [
        {
            "amount": 15462131,
            "size": 154621310000,
            "google_earth_amount": 45614157,
            "id": "datapool_id",
            "max_latitude": 68.3,
            "max_longitude": 135.7,
            "min_ longitude": -20.7,
            "min_latitude": -30.3,
            "type": 2
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
 | ----------- | ------------ |------------ |------------ |------------ |
 | name | string | 数据池名称 | 是 |  | 
 | db_type | string | 数据类型 | 是 |  | 
 | max_longitude | float64 | 最大经度 | 是 | ±164.8 | 
 | min_ longitude | float64 | 最小经度 | 是 | ±32.7 | 
 | max_latitude | float64| 最大纬度 | 是 | ±68.9 | 
 | min_latitude | float64 | 最小纬度 | 是 | ±31.2 | 
 | disk_uuid | string | 磁盘id | 否 |  | 

请求示例：
```json
{
    "datapool": {
        "ll_bound": {
            "max_latitude": 68.3,
            "max_longitude": 135.7,
            "min_ longitude": -20.7,
            "min_latitude": -30.3
        },
        "name": "HongKong",
        "db_type": "ifile",
        "disk_uuid": "e397d049-7b61-4452-bf04-3b91f82dc51c"
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
 | ----------- | ------------ |------------ |------------ |------------ |
 | max_longitude | float64 | 最大经度 | 是 | ±164.8 | 
 | min_ longitude | float64 | 最小经度 | 是 | ±32.7 | 
 | max_latitude | float64 | 最大纬度 | 是 | ±68.9 | 
 | min_latitude | float64 | 最小纬度 | 是 | ±31.2 | 
 | db_type | string | 数据类型 | 是 |   | |

请求示例：
```json
{
    "max_longitude": 135.7,
    "min_ longitude": -20.7,
    "max_latitude": 68.3,
    "min_latitude": -30.3,
    "db_type": "tfile"
}

```
响应数据：

 | 响应参数 | 类型 | 参数说明 | 是否必选 | 备注 | 
 | ----------- | ------------ |----------- |----------- |----------- |
 | cap | uint64 | 剩余磁盘空间 | 是 |  返回字节数  |
 | uuid | string |  | 是 |    || 
 
响应示例：
```json
{
    "commserv": [
        {
            "cap": 3448653416,
            "uuid": "d0h5-as9ee45d4c4fd6e"
        },
        {
            "cap": 34486534216,
            "uuid": "de5c-5w3a37yua632fda"
        }
    ]
}

```
