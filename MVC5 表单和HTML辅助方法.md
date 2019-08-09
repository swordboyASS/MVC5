### HTMl形式  
```
<form action=“网址” method=“get/post”>
    控件标签
</form>
````

action告诉大家表单信息发往哪里
method告诉大家数据的发送模式主要是get和post方法

### get方法和post方法  
get方法：传送数据长度有限，可以保持数据，能够将表单数据可以作为发送地址参数发送
post方法：可以传送大量数据，能改变服务器状态
常用方法是get常用作查询，读取，post常用作修改、添加、删除。

### HTML.BeginForm辅助方法   
代替了我们的html中的form标签，配合mvc框架使用
Html.BeginForm(“方法”,”mvc控制器名称”，Method)

### 实例
创建Test控制器=》 添加Test视图=》在视图中创建form表单，写一个text标签和submit标签=》text标签的name属性和action中控制器的方法参数对应相同。

视图中的代码：
![b1](https://github.com/swordboyASS/MVC5/blob/master/picture/b1.png)



添加target属性使用Html辅助方法，对比传统方式：
![](https://github.com/swordboyASS/MVC5/blob/master/picture/b2.png)

### Html.HIdden("控件名","控件值")

`它会隐藏在后台，当触发的特定事件时才会“显性”`
第一个参数表示 它自身的name属性，第二个表示它name属性的值，类似于键值对 name：key，值：value

### Html.Label() 和 Html.TextBox（）

分别替换label标签和text属性
![](https://github.com/swordboyASS/MVC5/blob/master/picture/b3.png)

### Html.DropDownList 和Html.ListBox

`Html.DropDownList/Html.ListBox 可以单选/主要是替换<select>`
	
![](https://github.com/swordboyASS/MVC5/blob/master/picture/b4.png)

![b5](https://github.com/swordboyASS/MVC5/blob/master/picture/b5.png)

取得是Value值 而非Key值
![b6](https://github.com/swordboyASS/MVC5/blob/master/picture/b6.png)

#### Home控制器

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;

namespace WebApplication0201.Controllers
{
    public class HomeController : Controller
    {
        public ActionResult Index()
        {
            return View();
        }

        public ActionResult About(string h1, string text1, string ddl1)
        {
            ViewBag.Message = h1 + "" + text1 + "/性别：" + ddl1;

            return View();
        }

        public ActionResult Contact()
        {
            ViewBag.Message = "Your contact page.";

            return View();
        }
    }
}

```

#### Test控制器

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using WebApplication0201.Models;
namespace WebApplication0201.Controllers
{
    public class TestController : Controller
    {
        //
        // GET: /Test/
        public ActionResult Index()
        {
            List<SelectListItem> slli=new List<SelectListItem>();
            SelectListItem s1=new SelectListItem();
            s1.Text="男";
            s1.Value="1";
            SelectListItem s2=new SelectListItem();
            s2.Text="女";
            s2.Value="2";
            slli.Add(s1);
            slli.Add(s2);
            ViewData["items"] = slli;
            return View();
        }
	}
}
```

#### 模型中的Calss1类

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;

namespace WebApplication0201.Models
{
    public class Class1
    {
        public string name{get;set;}
        public string value { get; set; }
    }
}
```

#### Test控制器的index视图

```C#
@model IEnumerable<WebApplication0201.Models.Class1>
@{
    ViewBag.Title = "View1";
}

<h2>View1</h2>
@*<form action="/Home/About" method="get" target="_blank">
    <input type="text" name="name1" />
    <input type="submit" value="搜索" />
</form>*@
@using (Html.BeginForm("About", "Home", FormMethod.Get, new { target = "_blank" })) { 
      
    @Html.Hidden("h1", "我是小明")
    <div>@Html.Label("lb1", "请输入：")
         @Html.TextBox("text1", "")</div>
    <div>
        @Html.Label("lb2", "性别：")
        @Html.ListBox("ddl1", ViewData["items"] as List<SelectListItem>, "请选择")
    </div>
    <input type="submit" value="搜索" />
}
```


好的学习者都习惯实践

![b7](https://github.com/swordboyASS/MVC5/blob/master/picture/b7.png)

没有默认值（虽然这么说，但真实不选其他的话没有默认值，只是提供了一个虚假的显示罢了）
//因为浏览器缓存原因，可能数据替换有延迟
 
 
 ### Html.Password()

前端：
![b8](https://github.com/swordboyASS/MVC5/blob/master/picture/b8.png)

后端：
![b9](https://github.com/swordboyASS/MVC5/blob/master/picture/b9.png)

### HTML.RadioButton（）和HTML.CheckBox（）
前端：
![b10](https://github.com/swordboyASS/MVC5/blob/master/picture/b10.png)

后端：
![b11](https://github.com/swordboyASS/MVC5/blob/master/picture/b11.png)

    
    
    
    
