# US3CLI 命令行工具

- [简介](#简介)

- [常用命令](#常用命令)

- [下载](#下载)
- [快速使用](#快速使用)

- [Linux](#Linux环境)

-    [Windows](#Windows环境)

-    [Mac](#Mac环境)

- [使用说明](#使用说明)

### 简介

us3cli 是用来在命令行上管理 US3 数据的工具，支持丰富的存储空间（bucket）以及对象（object）操作，支持Windows、Linux、Mac平台。

通过本工具，您可以进行以下操作：

存储空间（bucket）：查看存储量，查看存储空间列表等。

对象（object）：上传、下载、删除、移动、拉列表、计算 etag 等。

另外，本工具提供丰富的批量操作：上传，下载，删除，拷贝，移动（同个存储空间内），数据取回等

### 常用命令

| 名称                | 功能                                                         |
| ------------------- | ------------------------------------------------------------ |
| [cat](#cat)         | 用于下载US3对象到标准输出                                    |
| [config](#config)   | 提供配置的创建、切换、删除、查看、更新                       |
| [cp]($cp)           | 用于对象的上传、下载、拷贝、秒传                             |
| [du](#du)           | 用于查看存储空间的存储量                                     |
| [etag](#etag)       | 用于查看本地文件、输入流、US3文件的etag                      |
| [ls](#ls)           | 用于获取Bucket列表、Object列表                               |
| [mb](#mb)           | 用于创建存储空间（Bucket）                                   |
| [mkdir](#mkdir)     | 用于在存储空间（Bucket）中创建目录                           |
| [modify](#modify)   | 用于修改对象（Object）的元数据（Metadata）、多媒体文件格式（MIME-TYPE）、存储类型 |
| [mv](#)             | 用于对象（Object）的移动                                     |
| [rb](#rb)           | 用于存储空间（Bucket）的删除                                 |
| [rcat](#rcat)       | 用于上传流式文件到US3                                        |
| [restore](#restore) | 用于归档类型对象的数据取回                                   |
| [rm](#rm)           | 用于对象（Object）的删除                                     |
| [sign](#sign)       | 用于获取对象的下载URL                                        |
| [stat](#stat)       | 用于查看对象（Object）、存储空间（Bucket）的具体信息         |
| [sync](#sync)       | 用于对象（Object）的增量上传                                 |
| [update](#update)   | 用于us3cli版本的更新                                         |
| [version](#version) | 用于查看us3cli版本信息                                       |

### 下载

当前版本：1.0.0

运行环境：Windows、Linux、Mac

下载链接：

[us3cli-linux64](http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-linux64)

[us3cli-win32.exe](http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-win32.exe)

[us3cli-win64.exe](http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-win64.exe)

[us3cli-mac](http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-mac)

### 快速使用

##### Linux环境

1.下载

```
wget http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-linux64
```

2.添加执行权限

```
chmod +x us3cli-linux64 
```

3.创建配置

```
us3cli-linux64 config
```

##### Windows环境

以下命令以Windows 64为例

1.[点击下载](http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-win64.exe)

2.打开cmd面板，切换到us3cli-win64.exe文件所在路径

3.执行config命令创建配置

```
us3cli-win64 config
```

##### Mac环境

1.使用curl下载

```
curl -o us3cli-mac http://ufile-release.cn-bj.ufileos.com/us3cli/us3cli-mac
```

2.添加执行权限

```
chmod +x us3cli-mac
```

3.配置

```
us3cli-mac config
```

### 使用说明

以下使用说明示例中本地文件路径均基于linux，使用命令时需要根据操作系统自行调整。

#### config

config命令用于创建配置文件。

##### 命令格式

```
us3cli config  [--ls][--su <configname>][--rm <configname>][--cat <configname>][configname]
			   [--accesskey <API/Token公钥>][--secretkey <API/Token私钥>][--endpoint <访问域名>]
```

##### 参数说明

```
-a,--accesskey:用于访问us3的API密钥或Token公钥
-s,--secretkey:用于访问us3的API私钥或Token私钥
-e,--endpoint:固定域名，可在地域和域名页查看
   --cat:打印指定配置项内容
   --ls:列出当前所有配置项
   --rm:删除指定配置项
   --su:切换指定配置为默认配置
```

配置文件内容说明：

| 配置项    | 说明                 | 填写说明                                                     |
| --------- | -------------------- | ------------------------------------------------------------ |
| AccessKey | 用于鉴权的bucket公钥 | [API公钥](https://console.ucloud.cn/uapi/apikey) 、[Token公钥](https://console.ucloud.cn/ufile/token) |
| SecretKey | 用于鉴权的bucket私钥 | [API私钥](https://console.ucloud.cn/uapi/apikey) 、[Token私钥](https://console.ucloud.cn/ufile/token) |
| Endpoint  | 外网或内网域名       | [地域和域名](https://docs.ucloud.cn/ufile/introduction/region) |

##### 使用示例

1.交互式配置

- 创建配置项

```
# us3cli config
输入当前配置项名称: config1
创建配置项
请输入API公钥[当前:]: TOKEN_13be86*********
请输入API私钥[当前:]: BAtrQO8LYdgve1HS_benbK-MXNTl3**********
地区列表：
No.     RegionName      Region      
0       北京             cn-bj       
1       上海二           cn-sh2      
2       香港             hk          
3       广东             cn-gd       
4       洛杉矶           us-ca       
5       新加坡           sg          
6       首尔             kr-seoul    
7       尼日利亚         afr-nigeria 
8       台北             tw-tp       
9       圣保罗           bra-saopaulo
10      迪拜             uae-dubai   
11      越南             vn-sng      
12      孟买             ind-mumbai  
13      华盛顿           us-ws       
14      法兰克福         ge-fra      
请输入region编号: 0
内外网列表：
No.     Network
0       外网   
1       内网   
请选择或输入内外网编号：0
您选择的endpoint是：[cn-bj.ufileos.com],[当前:]，请输入回车确认或自定义endponit：

当前最终配置:
ConfigName: config1
AccessKey: TOKEN_13be86*********
SecretKey: BAtrQO8LYdgve1HS_benbK-MXNTl3**********
Endpoint: cn-bj.ufileos.com

是否使用该配置作为默认配置(当前默认配置为：<configtest>)(y or n)? y
```

注：首次创建的配置文件时会自动将该配置作为默认配置

- 列出配置项列表

说明：

1.Default标识表示该配置项是当前的默认配置

2.Authority表示权限分类，只用于快速区分Token和API密钥格式，不保证内容准确

```
# us3cli config --ls
ConfigName              ModTime                 FilePath                         Authority                 
config1  (Default)      2020-09-21 14:18:50     /root/.us3cliconfig/config1      Token       
config2                 2020-09-21 14:18:50     /root/.us3cliconfig/config2      Token     
us3cli                  2020-09-16 10:36:00     /root/.us3cliconfig/us3cli       APIKey
```

- 切换配置项

```
# us3cli config --su config2
Default configuration has been changed to  [ config2 ]
# us3cli config --ls
ConfigName              ModTime                 FilePath                         Authority                 
config1                 2020-09-21 14:18:50     /root/.us3cliconfig/config1      Token      
config2  (Default)      2020-09-21 14:18:50     /root/.us3cliconfig/config2      Token  
us3cli                  2020-09-16 10:36:00     /root/.us3cliconfig/us3cli       APIKey
```

- 删除配置项

```
# us3cli config --rm config1
Deleting configuration file  [ config1 ] , whether to continue(y or n) ? y
Configuration file [ config1 ] has been deleted
```

注：以下所有命令的（y or n）选项规则均不区分大小写，输入yes或y表示确认，其他选项均表示取消

- 打印配置项

```us3cli config --cat config2
# us3cli config --cat config2
AccessKey: TOKEN_13be86*********
SecretKey: BAtrQO8LYdgve1HS_benbK-MXNTl3**********
Endpoint: cn-bj.ufileos.com
```

2.非交互式配置

```
# us3cli config config3 --accesskey TOKEN_AAGASGAZVZV**** --secretkey USAsflmTAAF****** --endpoint cn-bj.ufileos.com
Configuration file [ config3 ] has been updated
```

3.临时使用（对其他命令生效）

- 上传文件时临时使用配置项config3

```
# us3cli cp test.txt us3://bucket1 --config config3
```

- 上传文件时临时使用配置文件 /home/ubuntu/myconfig1

```
# us3cli cp test.txt us3://bucket1 --config /home/ubuntu/myconfig1
```

- 上传文件时使用自定义配置内容

```
# us3cli cp test.txt us3://bucket1 --accesskey LTAI4G3t3BTza47xxxxxxxxxx --secretkey gznFs9daMtKmUaTq9xpxxxxxxxxxxxxx --endpoint cn-bj.ufileos.com
```

#### cat

本命令用于流式下载文件，

##### 命令格式

```
us3cli cat us3://<bucketname>/<keyname> [--retrycount <重试次数>][--speedlimit <速度限制>]
```

##### 参数说明

```
     --retrycount: 失败重试次数,默认值：10
 -s, --speedlimit: 平均速度限制(单位可以是B,KB,MB，不带单位默认以B/s计算)，默认200MB/s
```

注：本工具所有的数据传输默认情况下均为不限速，单位可以是B/KB/MB或直接输入数字，数字以B/S 计算，这里所有的B均指字节。

##### 使用示例

- 查看test.txt文件内容

```
us3cli cat us3://bucket1/test.txt
```

- 流式下载test.txt到本地

```
# us3cli cat us3://bucket1/test.txt > test.txt
```

- 流式下载并限速为1MB/s

```
# us3cli cat us3://bucket1/test.txt --speedlimit 1MB > test.txt
```

- 流式下载并设置重试次数为5次

```
 us3cli cat us3://bucket1/test.txt --retrycount 5 > test.txt
```

#### cp

该命令用于上传、下载、拷贝文件

##### 命令格式

上传文件

```
us3cli cp <本地文件路径> us3://<存储空间名称>/<文件Key> [-r][--hit modtime|etag][--parallel <分片上传并发数>][--speedlimit <速度限制>][--storageclass <存储类型>][-exclude <通配符表达式>][--rexclude <正则表达式>][--include <通配符表达式>][--rinclude <正则表达式>][--metadata <Key>=<value1>[,<key2>=<value2>]...][--mimetype <多媒体文件格式>]
```

下载文件

```
us3cli cp us3://<存储空间名称>/<文件Key> <本地文件路径> [-r] [--speedlimit <速度限制>][--exclude <通配符表达式>][--rexclude <正则表达式>][--include <通配符表达式>][--rinclude <正则表达式>]
```

拷贝文件

```
us3cli cp us3://<存储空间名称>/<文件Key> us3://<存储空间名称>/<文件Key> [-r][-exclude <通配符表达式>][-rexclude <正则表达式>][-include <通配符表达式>][-rinclude <正则表达式>][--metadata <Key>=<value1>[,<key2>=<value2>]...]
```

##### 参数说明

```
-r	--recursive:递归文件夹中的所有文件及子目录下所有文件
	--hit: 秒传文件，无默认值
		modtime:在判断是否上传时采用文件最后修改时间作为判断标准，如果本地文件最后修改时间晚于us3，则进行上传请求，否则不上传
    	etag:在判断是否上传时采用文件etag作为判断标准，如果本地文件etag和us3中的etag不同，则进行上传请求，否则不上传
-s, --speedlimit: 平均速度限制(单位可以是B,KB,MB，不带单位默认以B/s计算)，默认200MB/s
	--storageclass：指定存储类型,对应有效值：STANDARD, IA, ARCHIVE(该参数仅限上传)，默认值：STANDARD
	--exclude: 不包含当前通配符的文件名
	--rexclude:不包含当前正则表达式的文件名
	--include: 包含当前通配符的文件名
	--rinclude:包含当前正则表达式的文件名
	--metadata:指定元数据信息(该参数仅限上传和拷贝) 多个元数据以","分隔，如 "key1=value,key2=value2",其他分隔符暂不支持
	--mimetype:指定mimetype(该参数仅限上传)
```

注：

1.通配符表达式暂时只支持“*”,"?"两种字符，并且需要注意的是，四种表达式筛选均以当前目录下文件路径为准

 如：   us3://us3cli/test 目录下的test2/test3.txt  会以test2/test3.txt作为字符串筛选，而不是以test3.txt作为字符串进行筛选

2.以下所有speedlimit选项均描述为平均速度

##### 使用示例

- 上传单个文件

```
# us3cli cp  ~/go/src/test.txt  us3://bucket1/test
```

- 上传单个大文件并设置分片并发数为10

```
# us3cli cp  ~/go/src/test.mp4  us3://bucket1/test --parallel 10
```

- 下载单个文件

```
# us3cli cp  us3://bucket1/test/test.txt  ~/go/src
```

- 拷贝单个文件

```
# us3cli cp  us3://bucket1/test.txt  us3://bucket2/test.txt
```

- 拷贝文件夹

```
# us3cli cp us3://bucket1/test	us3://bucket2/test
```

- 下载文件夹

```
# us3cli cp  -r us3://bucket/test   ~/go/src
```

- 秒传文件

```
# us3cli cp  ~/go/src/test  us3://bucket/test --hit etag
```

- 指定存储类型上传

上传单个文件并指定存储类型为IA（低频访问）类型

```
# us3cli cp ~/go/src/test.txt  us3://bucket/path --storageclass IA
```

- 限速上传

上传文件test.txt，并设置速度为1024Kb/s

```
# us3cli cp ~/go/src/test.txt us3://bucket/test --speedlimit 1024Kb
```

- 限速下载

下载文件test.txt，并设置速度为1024Kb/s

```
# us3cli cp us3://bucket/test ~/go/src/test.txt --speedlimit 1024Kb
```

- 批量上传

上传所有格式为jpg的文件（通配符）

```
# us3cli cp ~/go/src/test us3://bucket/test --include "*.jpg"
```

上传所有a开头b结尾的文件(正则表达式)

```
# us3cli cp ~/go/src/test us3://bucket/test --rinclude "a*b"
```

上传所有不包括a开头b结尾的文件(正则表达式)

```
# us3cli cp ~/go/src/test us3://bucket/test --rexclude "a*b"
```

上传所有文件名不包括001的文件（通配符）

```
# us3cli cp ~/go/src/test us3://bucket/test --exclude "*001*"
```

- 上传单个文件并指定元数据信息

```
# us3cli cp ~/go/src/test us3://bucket/test --metadata key1=value1,key2=value2
```

- 指定mimetype为text/plain上传

```
# us3cli cp ~/go/src/test us3://bucket/test --mimetype text/plain
```

#### du

该命令用于获取指定存储空间(Bucket)各存储类型的存储量大小，以及总存储量

注：存储量结算时间为当前日期前一天0:00

##### 命令格式

```
us3cli du us3://<存储空间名称>
```

##### 使用示例

- 查看bucket1所占空间大小，内容包含各存储类型的存储量以及总存储量

```
StorageClass    Size   
STANDARD:       1.05 GB
IA:             0 GB   
ARCHIVE:        0 GB   
Total storage:  1.05 GB
```

#### etag

该命令用于计算文件etag值

##### 命令格式

```
us3cli etag [<本地文件路径1>,[<本地文件路径2>] ...] [us3://<存储空间名称>/<文件Key>] [-]
```

##### 参数说明

```
-:计算标准输入中的数据流etag值
```

##### 使用示例

- 计算本地文件etag值

```
# us3cli etag main.go
Name              Etag                            
main.go           AQAAAEpmwm87EANJQDpLTEmxsjR7-R0N
test.go       	  AQAAAA2_k04RGgAoswywP94gVsmsRph1
```

- 计算us3文件etag值

```
# us3cli etag us3://bucket1/test.txt
Etag: AQAAAEpmwm87EANJQDpLTEmxsjR7-R0N
```

- 计算标准输入etag值

```
# cat test.txt | us3cli etag -
Name    Etag                        
-       SmbCbzsQA0lAOktMSbGyNHv5HQ0=
```

- 计算多个文件etag

```
# cat test4.txt | us3cli etag us3://bucket1/test.txt us3://bucket1/test2.txt test3.txt -
Name                                    Etag                            
us3://bucket1/test.txt                  AQAAAEpmwm87EANJQDpLTEmxsjR7-R0N
us3://bucket1/test2.txt                 AQAAAEpmwm87EANJQDpLTEmxsjR7-R0N
test3.txt    							AQAAAHPuBl-6VRpzVHiBFjSOVhLrcsam
-                                       SmbCbzsQA0lAOktMSbGyNHv5HQ0= 
```

#### ls

该命令用于列出存储空间(Bucket)、对象（Object）

##### 命令格式

```
us3cli ls [us3://<存储空间名称>] [--limit <输出限制数>][--restore][--delimiter]
```

##### 参数说明

```
-r,--restore: 是否展示数据解冻信息
-l,--limit:   需要同时列出的最大文件条数
   --flat:    是否以非层级结构显示,默认层级显示
```

##### 使用示例

- 列出当前权限下所有bucket

```
# us3cli ls
BucketName      Region  Acl     CreateTime         
bucket1     	cn-bj   public  2020-03-27 17:20:56
bucket2      	cn-bj   private 2020-03-27 17:20:43
us3cli          cn-bj   public  2020-09-15 16:17:24
```

- 列出bucket下所有对象

```
# us3cli ls us3://bucket
Key                     FileSize   StorageClass         Etag                             CreateTime      
us3://bucket/cf1   		DIR        IA                   AQAAANo5o-5ea0sNMlW_75VgGJCv2AcJ 2020-07-16 18:51:04  
us3://bucket/aa.txt     4KB        STANDARD             AQAAAGNlfLt9cIbFawzU5caZm7aDZkho 2020-07-22 11:04:34 
us3://bucket/aa.txt     4KB        ARCHIVE              AQAAAGNlfLt9cIbFawzU5caZm7aDZkho 2020-07-22 11:04:34 
```

- 列出bucket下对象并限制显示文件数量为2

```
# us3cli ls us3://bucket --limit 2
```

- 列出bucket下对象并显示数据解冻状态信息

```
# us3cli ls us3://bucket --restore
```

- 递归当前文件列出非目录形式的文件列表

```
# us3cli ls us3://bucket --delimiter
```

#### mb

该命令用于创建存储空间

##### 命令格式

```
us3cli mb us3://<存储空间名称>  [--acl <权限类型>][--region <桶所在地区>][--projectid <项目ID>]
```

##### 参数说明

```
-a,--acl:      权限类型，可以设置为private、public，默认为private私有。
-r,--region:   桶所在地区，可查看地域信息，默认地区为北京。
-p,--projectid:项目ID，当前bucket属项目ID，默认为Default
```

本命令提供命令输入和交互式输入二选一的操作，命令输入参数，就会自动跳过交互式输入。

##### 使用示例

- 交互式创建bucket

```
# us3cli mb us3://us3cli-testr
请输入要创建bucket的权限类型acl(Private/Public,默认为Private):public
地区列表：
No.     RegionName      Region      
0       北京            cn-bj       
1       上海二          cn-sh2      
2       香港            hk          
3       广东            cn-gd       
4       洛杉矶          us-ca       
5       新加坡          sg          
6       首尔            kr-seoul    
7       尼日利亚        afr-nigeria 
8       台北            tw-tp       
9       圣保罗          bra-saopaulo
10      迪拜            uae-dubai   
11      越南            vn-sng      
12      孟买            ind-mumbai  
13      华盛顿          us-ws       
14      法兰克福        ge-fra      
请输入要创建bucket地区编号或地区代码(默认为北京:cn-bj):0
Region: cn-bj
当前账号下业务组分组信息如下：
No.     ProjectName     ProjectId 
1       Default         org-orcwsj
请输入要bucket的项目编号:1
Number: 1
ProjectID: org-orcwsj
Make bucket [ us3cli-test ] success
```

- 非交互式创建bucket,输入acl，region以及projectid信息，acl,region是必填项，projectid可不填

```
# us3cli mb us3://us3cli-test --acl private --region cn-bj --projectid org-orcwsy
Make bucket [ us3cli-test ] success
```

#### mkdir

本命令用于在us3存储空间内创建目录

##### 命令格式

```
us3cli mkdir [-d] us3://<存储空间名称>/<目录名>[/<目录名>]
```

##### 参数说明

```
-d：用于创建多级目录
```

##### 使用示例

- 创建目录

```
# us3cli mkdir us3://bucket/dir
```

- 创建多级目录

````
# us3cli mkdir -d us3://bucket/dir1/dir2
````

#### modify

该命令用于修改us3中的文件信息

##### 命令格式

```
us3cli modify us3://<存储空间名称>/<文件Key> [--storageclass <存储类型>][--mimetype <多媒体文件格式>][--metadata <<key1=value1>[,<key2=value2>]...>]
```

##### 参数说明

```
	--storageclass：指定存储类型,对应有效值：STANDARD, IA, ARCHIVE
	--metadata:指定元数据信息 
	--replace：是否清空原有元数据
	--mimetype:指定多媒体文件格式mimetype
```

##### 使用示例

- 存储类型改变

修改test.txt的存储类型为STANDARD标准型

```
# us3cli modify us3://bucket/test.txt --storageclass STANDARD
```

- mimetype改变

修改test.txt文件的mimetype信息

```
# us3cli modify us3://bucket/test.txt --mimetype image/x-icon
```

- metadata改变

1.修改test.txt文件的元数据信息，以key=value形式作为参数，可修改多个元数据信息，中间以英文逗号","分隔.

```
# us3cli modify us3://bucket/test.txt --metadata "key1=value1,key2=value2"
```

2.清除原有元数据，添加新的内容

```
# us3cli modify us3://bucket/test.txt --metadata "key1=value1" --replace
```

3.删除元数据

```
# us3cli modify us3://bucket/test.txt --metadata "" --replace
```

#### mv

本命令用于移动文件

注意：本命令只能用于相同bucket之内，同时-f选项只支持文文件

##### 命令格式

```
us3cli mv us3://<存储空间名称>/<文件Key> us3://<存储空间名称>/<文件Key> [--force]
```

##### 参数说明

```
-f,--force:存在同名文件时是否覆盖
   --parallel:并发数
   --exclude: 不包含当前通配符的文件名
   --rexclude:不包含当前正则表达式的文件名
   --include: 包含当前通配符的文件名
   --rinclude:包含当前正则表达式的文件名
```

##### 使用示例

- 移动文件

```
# us3cli mv us3://bucket/test.txt   us3://bucket/test/test.txt				
```

- 强制移动文件

```
# us3cli mv us3://bucket/test.txt   us3://bucket/test/test.txt -f
```

- 移动文件夹
- 注意：目标文件夹存在时，文件夹会被移动到目标文件夹子目录中

``` 
# us3cli mv us3://bucket/test  us3://bucket/test2  				
```

#### rb

本命令用于删除存储空间

##### 命令格式

```
us3cli rb us3://<存储空间名称>
```

##### 参数说明

```
-f,--force:强制删除
```

##### 使用示例

- 删除存储空间:存储空间必须为空，否则无法删除

```
# us3cli rb us3://bucket1
The bucket [bucket1] is being deleted, continue(y or n)? y
Delete bucket [bucket1] success
```

#### rcat

本命令用于流式上传文件

##### 命令格式

```
us3cli rcat us3://<存储空间名称>/<文件Key>	[-retrycount <重试次数>][--speedlimit <速度限制>][--parallel <并发数限制>]
```

##### 参数说明

```
-s, --speedlimit: 平均速度限制(单位可以是B,KB,MB，不带单位默认以B/s计算)，默认200MB/s
	--retrycount:分片失败重试次数，默认10次
	--parallel:大文件上传并发数
```

##### 使用示例

- 上传流式数据到us3中

```
# cat test.txt | us3cli rcat us3://bucket1/test.txt
```

- 流式上传文件test.txt并设置限速为 2MB/s

```
# cat test.txt | us3cli rcat us3://bucket1/test.txt --speedlimit 2MB
```

- 流式上传文件test.txt并设置重试次数为5次

```
# cat test.txt | us3cli rcat us3://bucket1/test.txt --retrycount 5
```

- 流式上传文件test.txt并设置并发数为2

```
# cat test.txt | us3cli rcat us3://bucket1/test.txt --parallel 2
```

#### restore

本命令用于恢复冷冻状态的对象（object）为可读状态

##### 命令格式

```
us3cli restore [-r] us3://<存储空间名称>/<文件Key>
```

##### 参数说明

```
-r,--recursive:递归文件夹中的所有文件及子目录下所有文件
-q,--qps:     限制请求数量，默认50qps，取值范围：1~1000
   --parallel:批量激活并发数，默认值为10
   --exclude: 不包含当前通配符的文件名
   --rexclude:不包含当前正则表达式的文件名
   --include: 包含当前通配符的文件名
   --rinclude:包含当前正则表达式的文件名
```

##### 使用示例

- 单个文件数据解冻

```
# us3cli restore us3://bucket/test.txt
```

- 数据解冻整个目录中所有文件

```
# us3cli restore -r us3://bucket/test
```

- 批量激活文件并设置并发数为30

```
# us3cli restore -r us3://bucket/test --parallel 30
```

#### rm

本命令用于删除目录或者对象

##### 命令格式

```
us3cli rm us3://<存储空间名称>/<文件Key> [-r][-f][--exclude <通配符表达式>][--rexclude <正则表达式>][--include <通配符表达式>][--rinclude <正则表达式>][--qps <每秒最大请求数量>]
```

##### 参数说明

```
-r,--recursive:递归删除目录及其内容，不区分大小写
-f, --force:   强制删除
-q,--qps:     限制请求数量，默认50qps，取值范围：1~1000
	--exclude: 不包含当前通配符的文件名
	--rexclude: 不包含当前正则表达式的文件名
	--include: 包含当前通配符的文件名
	--rinclude:包含当前正则表达式的文件名
	--parallel:批量删除并发数，默认值为10
```

##### 使用示例

- 删除文件

```
# us3cli rm us3://bucket/test.txt
The file [test.txt] is being deleted, continue(y or n)? y

1  files have been deleteed, 0  Successed, 0  Failed
```

- 强制删除文件

```
# us3cli rm us3://bucket/test.txt
1  files have been deleteed, 0  Successed, 0  Failed
```

- 强制删除文件夹

```
# us3cli rm -r -f us3://bucket/test
```

- 批量删除test文件夹中后缀名为.jpg的文件

```
# us3cli rm -r us3://bucket/test --include  "*.jpg" 
```

- 批量删除限速,以每秒请求数量为限制，最大可以上调到1000qps，取值范围在1~1000

```
# us3cli rm -r us3://bucket/test --include  "*.jpg" -qps 10
```

- 批量删除文件并设置并发数为30

```
# us3cli rm -r us3://bucket/test --parallel 30
```

- 清空bucket

```
#us3cli rm -r -f us3://bucket --parallel 10
```

#### sign

本命令用于文件下载url获取

##### 命令格式

```
us3cli sign us3://<存储空间名称>/<文件Key>   [--expires <时间>]
```

##### 参数说明

```
--expires:url使用的过期时间点,单位s
```

##### 使用示例

- 获取url签名

```
# us3cli sign us3://bucket/test.txt
```

- 获取限时100s 的url签名

```
# us3cli sign us3://bucket/test.txt --expires 100
```

#### stat

本命令用于查看存储空间或文件信息

##### 命令格式

```
us3cli stat us3://<存储空间名称>[/<文件key>]
```

##### 使用示例

- 查看bucket1的信息

```
# us3cli stat us3://bucket1
BucketName:     bucket1             
Region:         cn-bj              
BucketId:       ufile-dpgjzcn     
Type:           public             
CreateTime:     2020-09-15 18:17:24
ModifyTime:     2020-09-15 18:17:24
```

- 查看us3://bucket1/test.txt的文件信息

```
# us3cli stat us3://bucket1/aaa.txt
Name:                   aaa.txt           
X-Ufile-Create-Time:    Fri, 18 Sep 2020 10:09:05 GMT     
X-Ufile-Storage-Class:  STANDARD                          
Server:                 nginx/1.11.1                      
Date:                   Mon, 21 Sep 2020 11:17:56 GMT     
Content-Type:           application/octet-stream          
Accept-Ranges:          bytes                             
Etag:                   "AQAAAEpjpDD8COEdGg3uOeLfsR_ddQgc"
Content-Length:         4298                              
Last-Modified:          Fri, 18 Sep 2020 10:09:05 GMT     
Vary:                   Origin           
```

#### sync

本命令用于文件或目录的增量上传

##### 命令格式

```
us3cli sync <本地文件路径> us3://<存储空间名称>/<文件Key> [--mode cache|remote][--speedlimit <速度限制>][--retrycount <重试次数>][--exclude <通配符表达式>][--rexclude <正则表达式>][--include <通配符表达式>][--rinclude <正则表达式>]
```

##### 参数说明

```
-s, --speedlimit: 平均速度限制(单位可以是B,KB,MB，不带单位默认以B/s计算)，默认200MB/s
-m, --mode:  默认mode值：cache
		cache: 以本地缓存为标准，检查基于缓存的增量文件，同步us3端对应目录的文件，默认为该模式
		remote:以本地文件系统为标准，检查本地文件以及us3不同步的文件，补全或删除us3端对应目录的文件
    --ruler:   默认ruler值：modtime
    	modtime:在判断是否上传时采用文件最后修改时间作为判断标准，如果本地文件最后修改时间晚于us3，则进行上传请求，否则不上传
    	etag:在判断是否上传时采用文件etag作为判断标准，如果本地文件etag和us3中的etag不同，则进行上传请求，否则不上传
    --parallel:并发数，默认值为10
	--retrycount：上传失败重试次数
	--exclude: 不包含当前通配符的文件名
	--rexclude:不包含当前正则表达式的文件名
	--include: 包含当前通配符的文件名
	--rinclude:包含当前正则表达式的文件名
```

增量模式说明：

1.cache模式使用本地缓存，从本地上传到bucket成功的文件，都会被记录为上传成功文件，如果需要重新上传，可以选择删除当前用户目录下的.us3cliconfig/leveldb文件夹，使用命令时会自动创建新的文件夹。

2.remote模式下最终以本地文件为标准，保证bucket中的目标文件夹和本地同步，`以下场景会进行文件删除，请慎用`：

增量上传文件夹后，将本地文件删除，再次使用remote模式增量，会将bucket中的文件删除以保持US3 Bucket和本地同步

##### 使用示例

- 增量上传，默认只检查us3cli缓存相对us3增量的数据，忽略本地已上传但us3再次删除的文件

```
# us3cli sync /root/test us3://bucket/path
```

- 全量同步，检查所有不一致的文件并us3端文件与本地同步

```
# us3cli sync --mode remote /root/test us3://bucket/path 
```

- 限速为1024 Kb/s上传

```
# us3cli sync /root/test us3://bucket/path --speedlimit 1024Kb
```

#### update

本命令用于版本更新

注：本工具更新后会根据操作系统创建不同的可执行文件，更新后文件名与当前文件保持同步，windows下更新会产生临时文件，再次运行程序时自动清除

##### 命令格式

```
# us3cli update
```

##### 参数说明

```
-f,--force:忽略版本，强制更新
```

##### 使用示例

```
# us3cli update
Your version is not the latest version, do you update it now(y or n):y
Downloaded latest version package,saved as: us3cli-linux64
```

#### version

本命令用于查看工具版本

##### 命令格式

```
# us3cli version
```

##### 使用示例

```
# us3cli version
us3cli version 1.0.0
```