### HTMl形式  
`
<form action=“网址” method=“get/post”>
    控件标签
</form>

`
action告诉大家表单信息发往哪里
method告诉大家数据的发送模式主要是get和post方法

### get方法和post方法  
get方法：传送数据长度有限，可以保持数据，能够将表单数据可以作为发送地址参数发送
post方法：可以传送大量数据，能改变服务器状态
常用方法是get常用作查询，读取，post常用作修改、添加、删除。

### HTML.BeginForm辅助方法   
代替了我们的html中的form标签，配合mvc框架使用
Html.BeginForm(“方法”,”mvc控制器名称”，Method)
