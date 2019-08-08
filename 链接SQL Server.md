
## 链接字符换

在APP_Start中创建一个ConnData类
![](7.png)

 ```C#
using System;
using System.Collections.Generic;
using System.Data;
using System.Data.SqlClient;
using System.Linq;
using System.Web;

namespace WebApplication01.App_Start
{
    public class ConnData
    {
        public DataSet getData()
        {
            string myStr = "server=.;database=db_09;UId=sa;password=123456";//获取链接字符串
            SqlConnection myConn = new SqlConnection(myStr);
            myConn.Open();//打开数据库
            string sqlStr = "select * from tb_Student ";//定义查询字符串，！！注意修改表名
            SqlDataAdapter myDa = new SqlDataAdapter(sqlStr, myConn);//sql数据适配器
            DataSet myDs = new DataSet();//创建dataset
            myDa.Fill(myDs);//SqlDataAdapter填充DataSet

            return myDs;
        }
    }
}
```

#### 创建一个名为stroeController的自定义控制器，并引入刚刚创建的类
```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Mvc;
using WebApplication01.Models;
using WebApplication01.App_Start;
using System.Data;
namespace WebApplication01.Controllers
{
    public class stroeController : Controller
    {
        //
        // GET: /stroe/
        public ActionResult Index()
        {
            ConnData conn = new ConnData();
            DataSet ds = conn.getData();
            user u1 = new user();
            u1.Name = ds.Tables[0].Rows[0][0].ToString();
            u1.Age = 30;
            List<user> ulist = new List<user>();
            ulist.Add(u1);
            return View(ulist);
        }
	}
}
```
#### 在模型中创建user类

![](8.png)

```C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;

namespace WebApplication01.Models
{
    public class user
    {
        string name;

        public string Name
        {
            get { return name; }
            set { name = value; }
        }
        int age;

        public int Age
        {
            get { return age; }
            set { age = value; }
        }
    }
}
```
#### 在视图中引用user类
```C#
@using WebApplication01.Models;
@model IEnumerable<user>

@{
    ViewBag.Title = "Index";
}

<h2>Index新建的视图</h2>
<ul>
    @foreach (user a in Model)
    {
        <li>@a.Name</li>
    }
</ul>
```
### 然后在视图下Ctrl+F5
![](9.png)
![](10.png)
