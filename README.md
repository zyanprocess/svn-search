# 七、基于AI增强SVN文档库（难度★★★☆☆）

**赛题描述**

现有SVN中存放着几乎所有的需求、设计、手册等有价值文档，但文档内容无法被检索，导致知识积累不能被很好的利用。如将这些知识全部导入知识库，则存在安全、公司制度、成本等方面的问题。

本赛题希望选手借助大模型和MCP技术开发一款工具，帮助我们解决这一问题，在尽量少改动现有文档管理方式的前提下，让SVN的文档内容可被搜索。

**详细说明**

![image.png](https://alidocs.oss-cn-zhangjiakou.aliyuncs.com/res/4maOgXbg6YKeRlWN/img/78eb3e4b-875f-498e-ba82-93f69beffb37.png)

*   首先开发一个预处理程序，每天扫SVN新增和变动的文档，并通过API调用公司内部大模型来解析文档内容，生成摘要信息和标签，记录到关系型数据库中备查
    
*   在现有知识库中网页中增加问答功能，或开发一个IDE插件，该插件展示一个问答界面，并通过websocket与MCP客户端交互
    
*   部署一个开源的MCP客户端，例如DeepChat，接收插件发送的问题，并返回大模型给出的答案
    
*   当用户输入对SVN文档的查询要求时，首先通过API调用公司内部大模型来解析语义和任务拆解
    
*   大模型可以通过MCP来获取关系型数据库的内容，包括通过权限数据来确定查询人可以反问的文档范围，以及根据语义从摘要库中检索以缩小打开文件的范围
    
*   部署开源的MCP服务端，如office-editer-mcp用于读取svn上的文档内容，然后大模型解析文档内容并总结输出
    

**交付物要求**

在总交付物要求的基础上，满足以下要求：

•本赛题要求选手提交的作品可以是编程IDE插件，或者独立网页，实现通过大模型直接从SVN文档库中搜索文档内容的功能。

•要求能根据用户的自然语言输入，准确找到SVN库中与问题相关的文档，读取文档全文，并给出总结性回答。

•要求不能改变现有SVN文档管理模式。

•要求每个用户提问的回答来源必须符合该用户的SVN目录权限，不得超出用户权限获取文档。

•要求对问题历史和回答可追溯

•开发者除了提交符合要求的程序外，还需要提供必要的文档，包括详细设计、安装手册、使用手册等

**技能要求**

Python或Java

**赛题资料**

给开发者提供一个预设的SVN文档库，库中存放数量较大的预设文档。文档类型需要有多种不同的，例如设计类、手册类等。

给选手提供内部大模型一套，并开放API权限

**评分维度**

在总评分维度的基础上，该选题还会从以下方面考核：

1.方案设计评分：由专家对方案设计的合理性、普适性以及新颖性进行评分。

2.程序效果评价：评委通过随机输入文档检索问题，对选手提交的工具进行评测。根据回答效果打分。

3.性能评价：解析文档全文需要消耗大量token，如果方案设计存在不足，无法应对比较模糊的提问，可能导致大模型根据问题大范围的读取文档，导致算力浪费。因此读取文档数量、消耗的token数量和问题响应时间需要单独评价。

**验证方式**

专家评委随机输入问题，根据实际效果评价。这些问题需要是根据预设的文档能够找到答案的。

**赛题对接人**

财富-李铁刚（05166）
