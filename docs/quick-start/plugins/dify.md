# Dify

**Dify** 是一个开源的大语言模型（LLM）应用开发平台，旨在简化和加速生成式 AI 应用的创建和部署。它结合了后端即服务（BaaS）和 LLMOps 的理念，为开发者提供了用户友好的界面和强大的工具，使得即使是非技术人员也能轻松参与到 AI 应用的定义和数据运营中。为非技术用户提供零代码和低代码的开发方式，通过简单的配置和少量代码，快速构建和部署基于大语言模型的应用程序，降低了 AI 应用开发的门槛。

目前MinerU 与 Dify 联合研发的 MinerU 插件已在 Dify 市场上架，帮助用户搭建工作流，提供文档解析的工作。

使用请访问：https://dify.ai/zh

# 一、**新版MinerU Dify插件亮点 (v0.4.0)**

- **完美适配MinerU2**：全面兼容MinerU2的最新功能，释放顶尖的文档解析能力。
- **超高灵活性**：同时支持官方在线API和本地化部署的API（并向下兼容 1.x 版本）。
- **赋能工作流**：让Dify的Agent拥有强大的文档“读写”能力，轻松处理复杂任务。

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGRiYWFiNmNiMjYyMzg5NmRjODllZjZjNGVlMzRlN2Vfc0RFbGFsdGFnY1FnRkZLZngwZTZiajhRQnh0RnlrWUdfVG9rZW46UDZlQWJJUXRib29TUEZ4REd5UGNiWWwzbkFoXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

# **二、实战演练：两个案例带你快速上手**

空谈不如实战。下面我们通过两个典型场景，向你展示新版插件的强大之处。

### 准备

1. 在Dify插件页面安装MinerU插件（私有化部署的Dify同理）

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NjM0NjY4NmVmYTBlNjQzZGFmMDUxODFkZDhlZDEyYjJfSFJranpDcVlqNFdPR1dFeHVFSW9FNEFTTVNkS3p0TG5fVG9rZW46STBjdGJtVUh0b2RHY1R4VjBMQWNxTDc3bnZnXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

1. 填写API URL等信息

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NzZhNDg1ODI4ZGRiZjczZDgyYTAxMmFjYmQ4MDljZjdfRldob1R1NjRkbm5BZ05MeXJvWTdGNXh3SnZWcE1JQk5fVG9rZW46WXMyMmJadmRSb3p5Ymt4QW0zdGNTckRIbndmXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

使用官方API时令牌（Token）必须提供👆，使用本地部署API时令牌可不填写👇

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=YWNlNzlkYmNkZjZjOTljYzg0ZjAyOWViN2JhYWMxZDZfYndDeGtmTWdoWHVEdkVxQ3cyc1RWN1pxUzhvUjZydGxfVG9rZW46TkFDVGI0ZElFb25SeFF4Q05Yb2MzeDR2bkIxXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

### **案例一：解析单文件，搭建Chat PDF应用**

想借助AI与你的文档对话吗？跟着下面几步，轻松实现

#### 第一步：创建空白应用，选择“Chatflow”

输入应用名称与描述

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=MmFhMWExMGJlN2FhMGNiYjZhMWM3ZGFmYTk5ZGRlZTNfNFFhM1Zub05nRXBoak5WbEJIOWpScVFWeDdOUEZmeUZfVG9rZW46WjFUQ2JOdktJb2o1TUx4SUhMQ2NSa29NblFnXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第二步：创建的初始模板中，选择“开始”节点

字段类型选为单文件，填写变量名称（此处填为input_file）,支持文档类型选为文档与图片

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=OTgxMjdmYTM0NGU1MjQ5MWVjNDEyODg2MzgwMTRmNmNfOTlaUWR3ZEhza3dhTm1qNFdPMGJjbUx4eTAxR01GMDBfVG9rZW46UGp6YWJRcXZrb2d3SWJ4MVhGNmM4MGFabmpmXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第三步：添加工具节点——MinerU插件来解析上一步开始节点上传的文件

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=YmI1ZDQ5YWYxNzRlZTIxNTY1ODg1NGZkMWJhNzg0NzdfWGRBUGVRMUtxd1JqVEZWWXZDNTY5VldvM3U1eVZsWmxfVG9rZW46T1BkM2JXRkVobzNHVEd4SEJUMmNwQkJRbk1mXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第四步：设置MinerU的输入变量，选择上一步开始节点添加的 `input_file`

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=Yjk4YjE4YzNkZGFjZjg2NGExZTE2MmExZmY2YTJlYzNfTUdmVUFZVzM2UUcxOUlRVmpZVHdaRVlLZFkxbG52RUNfVG9rZW46WFRvbmIxekt5b2V1b0Z4YzY2ZWNSNlF3bnpiXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第五步：配置LLM模型

选择“LLM”节点后，如果没有模型可用，需要单独在插件市场安装（这里使用 Deepseek作为示例）

“上下文”选择MinerU的输出变量 `text`（MinerU解析文档后的markdown格式）

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=YTVkNmFmZGQ4MzBmY2FkNjY4MzhjZDFmNzI0ZThkNDlfVXYyRTZlNjBvQ2ZweGgxakNhRG90ZFBQZ1RzdklOeDJfVG9rZW46UDgwSGJpcUZGb2I3a1Z4NVhCSmNxVDNBblN0XzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

在“SYSTEM”区域根据实际需求填写提示词，可如图填写“在Parse File `text`中提取用户的问题答案”

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDBmMTBhMzdkOWM2YjAzODQyZWQ1MmNkN2VjNTI3ZmVfbWlIUDZqNlhzZ0l5ZUoyWEhpOHh4cWlqUWpwM3EwcTVfVG9rZW46UG5KVGJnbEsyb0ZOOW94Y3p1cGNqMjFObnVlXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第六步：预览，上传文件并提问机器人关于文档的内容

至此一个简单的文档问答应用Chat PDF搭建完成，点击“预览”，查看效果如何👇

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NzBkNTVjYmVkYWJjNDI1YzIzMGRiNDI0Yjk4N2NlNjlfbG84Zzk0dlJxR3RudTZSRG9sVTNSNjJRaVRPQ3dwN1BfVG9rZW46WnZLYmJCak9jb2FlUkN4UDdqRGM2V2dObmxoXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

结果如下：

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=N2NjY2Q1ZmUwZjVmNWVmZWViY2E0ZWZjYzg2ODIwOGVfZ0p0cjlsbFJqV0VNbXFPeHlTNzd0bVc0cGJvQVl6b0pfVG9rZW46VjFwQWJzT1JTb2FpRTF4R0pXeWNiVHU4bml1XzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### **第七步：发布与测试**

保存并发布你的应用。现在，上传一份PDF或图片，你就可以和它自由对话了！

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=YjIzNTdhYzExYzUxN2M5NjhmOWRhOTYwY2RhZjlhMGVfMnhYcmVicDM2NWVpN0JwT3plRUdWY1QwQWx0NHV5SnZfVG9rZW46VUZzMmJ6cGRMb01EVVl4S1U1eWN4aFZRblVmXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

### **案例二：自动化批量处理文档，并上传至云端S3**

需要处理大量文档并归档？MinerU 插件同样能胜任

#### 第一步：安装 botos3 插件

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NWIwYzc2MDQ2MDlmYzVjNDAxZjc2NjgzMmRlM2E5M2NfMEs5T2RFSHVVcWVrcEtFRTFucmRWbGpFcGMyS2lQNFVfVG9rZW46QzJ1NmJZT3M5b2N5VnN4RGlyOWNaaU1tbmdkXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第二步：配置 S3 bucket

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NjE4ZWU5ZTU5MGY5OGJiZGZkYWM5ZmVhY2RkNDkxYTdfcHlIcmx3b0FISDVRTkgyRTNzMEJucTV5bWlyY3dteFdfVG9rZW46VUtzbmI4Nm13b1F5ZVp4aEhOWWN3N21CbnBnXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第三步：创建工作流

选择字段类型为“文件列表”，填写变量名称（此处填为input_files）,支持的文档类型选为文档与图片

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=MzAyYmUxYzRiMjM5ZjgyOTBjOWQ5NzA4ODJlYzg1YThfNkFBUUpVY1JleDhYclZUYWh5YU5GZGt0WmpETkdDWjZfVG9rZW46R2oxaGJUR1pBbzdycjV4UGo4c2NPY1RmbndjXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第四步：添加“迭代”

在“开始”节点后添加“迭代”，并配置迭代内的MinerU节点,设置迭代的输入为上一步开始节点的`upload_files`，输出节点暂时不填写，再整个迭代配置完成后选择MinerU节点Parse File的`full_zip_url`

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjI3MjEwNzVmMDIxYmQxZGUwYWJiOGM1NTM4M2E0NWRfN1hLM0ZOUXR3OHhoM0RvQVZ5NDg1WDlwRlpPZ2E2MmRfVG9rZW46U3E5bWJhc0Ftb2JYRFd4R1hBYmNlODdGbnRoXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

将MinerU的输入参数file选择为迭代器的 `item`

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZTA1MmY0ZTczYTZjM2I3MTM4YTBhNGE2NzkxOTI0NDFfbHI2RmNOa3FDdFU4b2hkYmRmQ2ZTd2ZSOE9DZDlHSWNfVG9rZW46THlpdGIza055b0RpZWJ4STFxUmNOOG81bkJnXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=OTE2YWVkM2I1ZDM0MWY0MDJlMWE2ZWQ3OTU5MTViYzVfdERSaVZrblVOazUzZkVPYzZsVmhWd2UxMlN1eElKd29fVG9rZW46T2ZOQ2JpSFVGb09tMnV4QW5idGNWMHBKbjBnXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第五步：增加中间节点“代码执行”来转换MinerU的解析结果

**输入变量(变量名称需与代码定义一致)**

- **text：**选择MinerU Parse File的输出变量`text`
- **uploadFiles：**选择“开始”节点的文件列表`upload_files`，用来根据迭代的index索引下标找到对应的原始文件名
- **index：**迭代的下标索引，选择迭代器的`index`

**输出变量(变量名称需与代码定义一致)**

- **fileName：**String
- **base64：**String

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=Yzg2OTMxNjBmNWI1MTY5MjZhNDJmNTdmZmY2ZDZhZmFfMVNrSUNIRzRzWHFWRGhxUDNLZm9jalNZRmp1eTBIdmhfVG9rZW46WnhOb2Jqb3kwb2x4cVZ4R0Z6TmM0aklGbmxlXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

代码选择JavaScript，编写转换代码：

暂时无法在飞书文档外展示此内容

以下为Python版本：

暂时无法在飞书文档外展示此内容

#### 第六步：配置 Botos3 插件来上传内容

添加工具节点Botos3，选择“通过s3上传base64”

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=MDQyY2U2NTYyMjk1MTM4NWRjMzE2ZGZmMTk1NzAxNzJfcDdlTXhFOHdHT2xwM3NlS0tSU3JRTHlGOWpCV2puZVBfVG9rZW46WGVCTWJvQ1J4bzR5ek94WXh4aGNzVnQ1bm9nXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

文件base64选择代码执行（图中为**转换MINERU MD文本**）输出的base64字段

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=YWYyNDdmOTRlYTQ1MDAxZjg5MmNkYTJlMDgzZWZmOTFfUEJ1M2lPUlFCdVdoZlBlakFkT25ZYVBJVUhLTDlhQVhfVG9rZW46SG95ZmJsUzNZb2N5bGZ4SkdwSmM0dmgzblJkXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

S3对象key，S3 对象key填写文件存储的路径，在 botos3 插件配置界面已经填写了 bucket 名称，这里只需要填写在bucket下存储的目录即可。选择代码执行**（图中为转换MINERU MD文本）**的`fileName`

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=MmNmZDdjNTk5ODU1ZDM2OTJhZWE2YjE2M2Q5YzJkOWRfYk1DV0ZCNURtOWJmcVdySDJ5MVFMQkE2cVNGR0F6eDNfVG9rZW46RTZaU2JlQ0JJb2hyd054T2N0bWNCb1I2bmVoXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第七步：预览效果

连接结束节点，至此，一个简单的上传到s3的工作流配置完成，点击“运行”看看效果👇：

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDcxOTk5NTI5MWRiNWRjZWM1MTI3YjVjYTFlOGM4N2VfUExGRFE4bzl4aDlxRWVwTklsZmkxeVRBbXdIR0FqbVRfVG9rZW46WGdFNWJsOURSb2t4Nml4Y2VJYmMzUXQ1bjlmXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDlmYmJmNjBiN2E4YTI0Yzc3YmQ1YmRhMjI4YjU0NmZfRDJUSzVtRDBUNEROV25PUVFSbWE1TEVhNGFHcFRxQktfVG9rZW46QTIwQ2JBOGp3b3F6Um94bVB1dWNaYTUzbmZlXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)

#### 第八步：Vis3查看文档

运行结束，可通过[vis3](https://github.com/opendatalab/Vis3?tab=readme-ov-file#features)来查看S3桶内是否已上传解析后的md文件，Vis3使用可参考

[新工具开源！Vis3大模型数据可视化利器：填 AK/SK 直接预览 S3 数据，JSON/视频/图片秒开！本地文件也可用](https://mp.weixin.qq.com/s/p3rH4EaoJB-AK7RWeDvOhg)

![img](https://aicarrier.feishu.cn/space/api/box/stream/download/asynccode/?code=NGZiOWU1NzZhZGM2ZGU3NWRlMjVmYzQ4MmZlMGNhZmRfeXUzblAwcmNUTndHSHFGZUtrOEpocEpWeXp5a0ZsRUdfVG9rZW46RVZZdWJhNlYwb0RneEl4SkxBMWNRdG5NblhlXzE3NTY5NzE3NjE6MTc1Njk3NTM2MV9WNA)