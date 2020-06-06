# Orm

beego 提供内部的 Orm 模块来简化对于数据库的操作。目前支持的数据库有 MySQL、Sqlite、Postgres。

## Mysql
```go
import (
	"github.com/astaxie/beego/orm"
	_ "github.com/go-sql-driver/mysql"
)

// User -
type User struct {
	ID   int    `orm:"column(id)"`
	Name string `orm:"column(name)"`
}

func init() {
	// need to register models in init
	orm.RegisterModel(new(User))

	// need to register db driver
	orm.RegisterDriver("mysql", orm.DRMySQL)

	// need to register default database
	orm.RegisterDataBase("default", "mysql", "root:123456@tcp(127.0.0.1:3306)/beego?charset=utf8")
}

func main() {
	// automatically build table
	orm.RunSyncdb("default", false, true)

	// create orm object
	o := orm.NewOrm()
	o.Using("default")

	// data
	user := new(User)
	user.Name = "mike"

	// insert data
	o.Insert(user)
}
```

## 引用
示例代码地址：[https://github.com/beego-dev/beego-example/blob/master/orm](https://github.com/beego-dev/beego-example/blob/master/orm)