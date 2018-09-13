# FTP上传下载

> 这部分讲一下R4版本做的一个FTP上传下载通用方法。

## 代码位置

### 项目
`http://10.45.7.208/svnzqzhjt/platform_dev/ZSmartCity/trunk/zsmartcity-biz`

### 代码位置
`FtpController`: `com.ztesoft.zsmartcity.common.controller.FtpController`

`FTPUtil`: `com.ztesoft.zsmartcity.common.util.FTPUtil`

## 配置
配置是通过数据库表配置的，今后如果提升，建议改为配置文件

表名：`tc_sys_config`

需要配置参数：
PARAM_CODE : FTP_CONFIG 

PARAM_VALUE: {"hostName": "10.45.70.40","httpPort": "8080","userName": "drcuser","passWord": "ztesoft","uploadPath": "pic","port":"21"}

##  PARAM_VALUE 字段说明
这是一个JSON的字符串，例如：

```JS
    {"hostName": "10.45.70.40","httpPort": "8080","userName": "drcuser","passWord": "ztesoft","uploadPath": "pic","port":"21"}
```
各个节点说明：

节点名称 | 含义
------|-------
hostName | 主机地址
port | FTP端口号
httpPort | HTTP服务端口号
userName | 用户名称
passWord | 密码
uploadPath | 上传默认路径

## 代码使用

### `FtpController`
3个接口，分别对应上传和下载,获取ftp文件存储根目录（用于拼接http····访问路径）

#### `FtpController/upload` 文件上传接口
- `dir` 文件目录 例如XXX/XXX, 或者/XXX/XXX. 为空默认为/根路径。但不推荐为空！
- `fileName` 文件名称, 支持自动补全后缀, 例如XXX.png或XXX. 
若不指定，即为文件本来的名称

#### `FtpController/download` 文件下载接口
- `filePath` 文件路径
- `fileName` 下载到本地的文件名称

#### `FtpController/getFtpPicRoot` 获取Ftp上文件存放的目录的 http 路径
- 新增接口，在宁波应急系统中提供  其它系统如果需要，需要移植下FtpController代码

### `FTPUtil`
后台FTP使用的一个综合工具类

#### {FTPConfig} `getFTPConfig`
获取FTP数据库中的配置信息

#### {String} `getHttpUrl`
- `filePath` 数据库中存文件的地址

获取FTP服务器上 HTTP前缀URL，拼接上业务表的附件路径，即为附件HTTP路径

#### {boolean} `uploadFileByStream`
- `fileName` 上传到服务器的文件名
- `dir` 文件的目录
- `inputStream` 输入文件流

根据文件流上传到FTP服务器

#### {boolean} `downloadFile`
- `response` HttpServletResponse
- `filePath` 相对路径
- `fileName` 文件名称

下载文件

#### {byte[]} `getDownloadFileByteArray`
- `filePath` 文件路径

从FTP获取文件ByteArray

#### {String} `getFtpPicRoot` 
- `rootPath` 显示访问根路径

## 总结
这部分主要说明了，R4 版本FTP的配置和使用方法。
