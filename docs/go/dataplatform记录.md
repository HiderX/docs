# dataplatform记录

## many2many

```go
type DataSource struct {
	gorm.Model
	OwnerId              uint                  `gorm:"index;not null;default:0;comment:单位"`
	Owner                metadata.Organization `gorm:"foreignkey:OwnerId"`
	System               string                `gorm:"not null;default:'';comment:系统"`
	OriginalDataType     string                `gorm:"not null;default:'';comment:原始库类型"`
	OriginalDataIp       string                `gorm:"not null;default:'';comment:原始库地址"`
	OriginalDataAccount  string                `gorm:"not null;default:'';comment:原始库账号"`
	OriginalDataPassword string                `gorm:"not null;default:'';comment:原始库密码"`
	Name                 string                `gorm:"not null;default:'';comment:名称"`
	Description          string                `gorm:"not null;default:'';comment:描述"`
	TechnicalOwners      []user.User           `gorm:"many2many:datasource_technical" json:"datasource_technical"`
	ManagementOwners     []user.User           `gorm:"many2many:datasource_management" json:"datasource_management"`
	SecurityOfficers     []user.User           `gorm:"many2many:datasource_security" json:"datasource_security"`
	AuthorizationMode    string                `gorm:"not null;default:'';comment:授权模式"`
}
```

这里`gorm:"many2many:datasource_technical"` 中，`datasource_technical`仅仅表示连接表的名字，并不代表是`datasource`和`technical`的连接表，谁是谁的连接表，取决于在哪个结构体中关联了另一个结构体。例如，在`DataSource`结构体中，`TechnicalOwners`关联了`User`表，因此many2many的连接表是`DataSource`和`User`的连接表。而由于Gorm的自动重命名特性，`DataSource`在mysql中的表名为`data_source`，`User`在mysql中的表名为`user`。

> https://blog.csdn.net/kingsill/article/details/134796092

## 自定义表名

```go
type Organization struct {
	Model
	DepartmentId string `gorm:"uniqueIndex;not null;default:'';comment:部门编号"`
	Department   string `gorm:"not null;default:'';comment:部门名称"`
	ParentId     string `gorm:"index;not null;default:'';comment:上级部门编号"`
	Status       string `gorm:"not null;default:'';comment:部门状态"`
	IsSt         string `gorm:"not null;default:'';comment:是否实体"`
	Level        int    `gorm:"not null;default:0;comment:部门级别"`
}

func (Organization) TableName() string {
	return "metadata_organization"
}
```

上表在数据库中的名字是？答案是`metadata_organization`。

## 使用postman

### form

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/image-20240302153104121.png)

### token

接口需要认证才能使用，因此要在Authorization选单中进行配置

![](https://cdn.jsdelivr.net/gh/HiderX/pictures@main/uPic/%E6%88%AA%E5%B1%8F2024-03-02%2015.32.21.png)

token在前端登录后使用F12获取

## api

```go
auth.GET("/list", GetDataSource) // interface testing
auth.POST("/add", AddDataSource)
auth.DELETE("/remove/:id", DeleteDataSource)
auth.PUT("/update/:id", UpdateDataSource)
auth.GET("/getAllColumnInfo", GetAllColumnInfo) //查询所有外键数据
auth.DELETE("/removeColumnInfo/:id", DeleteColumnInfo)
```

### add

通过form传值，接受后绑定到`RequestDataSourceForm`结构体，其定义如下：

```go
type RequestDataSourceForm struct {
	OwnerId              string   `form:"ownerId" json:"ownerId"  binding:"required"`
	System               string   `form:"system" json:"system"  binding:"required"`
	OriginalDataType     string   `form:"originalDataType" json:"originalDataType"`
	OriginalDataIp       string   `form:"originalDataIp" json:"originalDataIp"`
	OriginalDataAccount  string   `form:"originalDataAccount" json:"originalDataAccount"`
	OriginalDataPassword string   `form:"originalDataPassword" json:"originalDataPassword"`
	Name                 string   `form:"name" json:"name"  binding:"required"`
	Description          string   `form:"description" json:"description"  binding:"required"`
	TechnicalOwnerIds    []string `form:"technicalOwnerIds" json:"technicalOwnerIds"`
	ManagementOwnerIds   []string `form:"managementOwnerIds" json:"managementOwnerIds"`
	SecurityOfficerIds   []string `form:"securityOfficerIds" json:"securityOfficerIds"`
	AuthorizationMode    string   `form:"authorizationMode" json:"authorizationMode"`
}
```

不难看出，`OnerId`、`System`、`Name`、`Description`为必填项，因此form表单至少应该如下：

|     Key     |  Value   |
| :---------: | :------: |
|   ownerId   |   0113   |
|   system    | testsys  |
|    name     | testname |
| description |   test   |

### list

列出所有的表项

可选参数（注意是通过query传值），如`list?name=testname`

```go
name := c.Query("name")   // get name param
owner := c.Query("owner") //获取单位数据
page := c.Query("page")
size := c.Query("size")
```

查询返回的结构体如下：

```go
type DataSource struct {
	gorm.Model
	OwnerId              uint                  `gorm:"index;not null;default:0;comment:单位"`
	Owner                metadata.Organization `gorm:"foreignkey:OwnerId"`
	System               string                `gorm:"not null;default:'';comment:系统"`
	OriginalDataType     string                `gorm:"not null;default:'';comment:原始库类型"`
	OriginalDataIp       string                `gorm:"not null;default:'';comment:原始库地址"`
	OriginalDataAccount  string                `gorm:"not null;default:'';comment:原始库账号"`
	OriginalDataPassword string                `gorm:"not null;default:'';comment:原始库密码"`
	Name                 string                `gorm:"not null;default:'';comment:名称"`
	Description          string                `gorm:"not null;default:'';comment:描述"`
	TechnicalOwners      []user.User           `gorm:"many2many:datasource_technical" json:"datasource_technical"`
	ManagementOwners     []user.User           `gorm:"many2many:datasource_management" json:"datasource_management"`
	SecurityOfficers     []user.User           `gorm:"many2many:datasource_security" json:"datasource_security"`
	AuthorizationMode    string                `gorm:"not null;default:'';comment:授权模式"`
}
```

其中`TechnicalOwners`、`ManagementOwners`、`SecurityOfficers`是分别从`datasource_technical`、`datasource_management`、`datasource_security`三张表查到的，根据`data_source`和`user`表的多对多映射。

### remove/:id

例子：`remove/30`，这里是通过更新gorm的`deleted_at`字段来实现软删除，如果要硬删除，加上：`db.Unscoped().Delete(&order)`

### update/:id

例子：`update/30`，form表单格式同`add`

### getAllColumnInfo



### removeColumnInfo/:id

