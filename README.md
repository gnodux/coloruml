# 基于PlantUML 的4色 领域模型建模


## coloruml

这个项目是在[PlantUML](http://plantuml.com)的基础上的定制，支持快速绘制领域模型图.

结合[C4 Model](http://c4model.com),基本可以实现从业务到技术架构的完整设计，C4 model参考另外一个项目: [C4-PlantUML](https://www.github.com/gnodux/C4-PlantUML)

PlantUML是一个开源项目，支持"写文字"的方式快速绘制多种图形UML及非UML图形。
具体语法可以参考：[PlantUML](http://plantuml.com)

## 关于4色领域模型建模

4色领域模型的概念来自 [Java Modeling In Color With UML](https://book.douban.com/subject/1440291/) 


_Peter Coad提出的几类基本元模型对于实际进行建模工作有着非比寻常的指导价值——当大多数人在分析业务领域模型时，Peter Coad在分析业务领域的元模型，其“鬼才”由此可见一斑。至于“带颜色的UML”，无非是对元模型的一种直观描述而已。对于面向对象（而非面向用例）的企业应用业务建模，这本“小书”便是首屈一指的最佳实践指南._

在这本小书里，archetype 被分为：

- Moment-Interval
- Role
- Description
- "Party,Place, or Thing"

4种类型。通过对对象的分类，快速抓住关键业务控制点。

领域模型建模的相关概念及链接:

* [https://www.infoq.cn/article/xh-four-color-modeling](https://www.infoq.cn/article/xh-four-color-modeling)
* [从“四色建模法”到“限界纸笔建模法”](https://insights.thoughtworks.cn/paper-pen-modeling/)
* [谈谈领域建模](http://fanyilun.me/2018/04/08/%E8%B0%88%E8%B0%88%E9%A2%86%E5%9F%9F%E5%BB%BA%E6%A8%A1/)

## Getting start

在绘制领域模型图的时候，直接引用:

```
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
```

例如一个简单的示例:

[Book Store](samples/bookstore.puml)

```csharp
@startuml Book Store sample

'!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml

!include ../coloruml.puml
'left_to_right

moment(订单,Order){
    int OrderId
    int Status

}
moment(Bill)
moment(Delivery)
thing(Book)
desc(Comments)
role(Customer)
thing(Employee){
    String Name
    Date Birthday
    int Status()
}
thing(Author)
role(Courier)
role(Accounting)

Courier from(Employee)
Accounting from(Employee)

Book contains(Comments)
Book has_d(Author)
Order contains(Bill)
Order contains(Delivery)
Order has(Book)
Bill has(Accounting)
Delivery has(Courier)
Customer has(Order)
Customer has(Comments)

Bill layout_u(Delivery)

@enduml
```
![Book Store](http://www.plantuml.com/plantuml/svg/NL4xJiGm4ErzYcorYOIIdcu_5Dj0iGU8J3ARMDYUrNWCH8WZK7813i2ja3W6Jh9EbhYmz6QUtvjvNYbRQLz3qZAVtMrHa7p96yMjV_GEg4BBO3clq1IDnTg_5XLg96zqOQHZe0ddvt09iLv5nJnVzDOQJbmobgIQbeKmQ89s-llzzVFnUVD0DL3s9f9mbELam8TwmaUMx9qGx_7TLccTHR07hPw1kanmgsoJRX6VCb63gz8TcfxYCa6e8Trvn-4DHUQTEMli02xMHwPGJUwbWG7l9KEoLSHjBRl5C6aMfXbLDfvRf6Y1dXH4jAagz9O3AnFYqafEX6Qs5ZDdsH7z9ad_3r9PTxNCK6-bA-l9V8Xiveu1BOfpK6CZA5p2wka3l1uuqeV6j5VCSAYE7_U_DeyvochPeUVINzd_0G00 "Book store")

## IntelliJ IDEA 集成

### IntelliJ IDEA
* 在JetBrains 下载IntelliJ IDEA [Download IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
* 安装Plugins: PlantUML Integration / PlantUML Syntax Checker

### Visual studio code

安装 [PlantUML extension](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)

## 开始绘制你的领域模型

### 引入定义模型定义

使用plantuml `include`预处理关键字引入模型

```csharp
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
```
### 领域对象的绘制

领域对象的绘制比较简单,使用封装的函数即可，以4色领域模型为例：

- moment(label,alias)|{}: moment-of-interval对象
- thing/party/place(label,alias)|{} : thing/party/place
- desc(label,alias)|{}: description描述对象
- role(label,alias)|{}: role 角色

```csharp
@startuml example
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
moment(订单,Order)
thing(书,Book)
@enduml
```


![example](http://www.plantuml.com/plantuml/svg/FSgn3S8m443HtbE4Bf6YkAUAM80PZ7rA8dntqVbEP0bA5g2Wf6SVa1W3LpHV-j8RYmPHmzp05d3Du7OBnMm9cbbrBNll9Lo6QT7PJbP08fC2wH0P_KISRFEHCujXzXYAWln_M6iSCbRVVf_tp_NM7oM1T4xdXQRs_Nhq1-PpvqQWLF4F)

接下来我们为领域对象添加一些属性和方法:

```csharp
@startuml example
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
moment(订单,Order)
thing(书,Book){
    string Title
    int AuthorId
    string ISBN
}
@enduml
```

![Field example](http://www.plantuml.com/plantuml/svg/JOqnQWCn44LxdKBfTc5PzQassssJ5Ca556bOYKYQPJGY2yP7SEaBk73ftlUnmSUmS64ynS1_FFuVCclY4eE4LSSbW7ZpoOHYGJhc9RyhHVg_dpsxybioaC74aBWt6DMSq9PL6Gn8jK95dHdecVkbFX4nLh-vdGxNtRxx8WlK2dO-pStbVEn6nBzs8sIzp5If_F4Su05yOlbHs25DzjMOliTFiHK395iNxW00)

### 领域模型的关系

主要包含以下关系:

- has: 可能包含
- contains: 父子关系
- rel: 引用

描述关系的时候使用has[_r/l/u/d],其中r(ight)/l(eft)/u(p)/d(own)可以进行简单布局。
contains和rel类似。 例如

```csharp
@startuml example
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
moment(订单,Order)
thing(书,Book){
    string Title
    int AuthorId
    string ISBN
}

Order has(Book)

@enduml
```

![relation example](http://www.plantuml.com/plantuml/svg/JOmnIWOn48NxEKNizeUVJM-rRhUD5dg1c0oRO3ApJ2Qu81x1qWjOMDfx7mMFOTX2VCM3z_7ufgfEj9LiS7TbomWNYNnk0KrKtUgbjU8UnpLfRFUjedWcHTBHSx4hSMYxzPnPki8MLnNbRuzRBoXSa7Ju-NZxVdaztqX0EO76HElmzVb-dfaVJazWUgfAf-OkQSO3959prJIoBE7_OxcTh-4Pu92PwEfmM00cfD1A_WK0)

更复杂的管理参考 [bookstore.puml](samples/bookstore.puml)

### 其他

#### 备注：可以给领域模型添加备注或说明


```csharp
@startuml example
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
moment(订单,Order)
note right of Order: 订单对象是有状态的
note left of Order
===订单对象流转说明
* 订单状态包含...
* 订单审批流程...
end note
@enduml
```

![notes examples](http://www.plantuml.com/plantuml/svg/SoWkIImgAStDKKYjICmjo4dbKipCIyufJKbLo2WfAIYsqjSlIYpNIyyioIXDAYrEBKhEpoj9pIlHIyxFrK_FoqyfhT1Fpi_9Bm8QeP-RM5oIMWJdwnK02QxS_5oWUeqNwnOzxPsgur-KabgaoPMNNvAgK9IPdb6Ya9-c01QqKe0eURf-vukD2v_DMFziJkVphctF6XgVpsg1QCX9JKEevxArjKNHiRNnnTurBzPlUJQZZqiBQXZ4WASzhKydhDRJquEBFrsty5ddJg2MvokwGUAfUIaA82ku780ieAi1)


### 预制函数

- hand_write():手写
- legend(): 图例
- hard_line(): 直线连接
- left_to_right() :从左到右布局
- title : 标题

```csharp
@startuml Book Store sample
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml

title 书店简单领域模型图

left_to_right()
hand_write()
hard_line()
legend()

moment(订单,Order){
    int OrderId
    int Status

}
moment(Bill)
moment(Delivery)
thing(Book)
desc(Comments)
role(Customer)
thing(Employee){
    String Name
    Date Birthday
    int Status()
}
thing(Author)
role(Courier)
role(Accounting)

Courier from(Employee)
Accounting from(Employee)

Book contains(Comments)
Book has_d(Author)
Order contains(Bill)
Order contains(Delivery)
Order has(Book)
Bill has(Accounting)
Delivery has(Courier)
Customer has(Order)
Customer has(Comments)

Bill layout_u(Delivery)
@enduml
```

![book store hand written](http://www.plantuml.com/plantuml/svg/NL4zZzGm4EtzAqoNI6ZJKztj7GKD5Fo0bOc7nCBshCPZZWYTH4M3A1454YUkG5JRGy6l8Npy2-nalO6ayfjvyzxCorbWHHoT5NUCRstK87lcVRZNDAIkDftXFZw90QX5p-1vqw9hEeywlcXQj4Xfj74gCD09R_PPZmrRa3--VXw_lVzrU3M-VVVdzlLuS_FpowVnuvlnmtSXUkNrxeeCGrKdG7fdZSzl2nrudHx2eKkkrU_3RHAu-uWqKFrIoFGPptB23_G9FsR5CGXnNUQsnjgwW4kmvZdGK0lkZU-gBUApMcW8RNM1BbD2BGWjL1SnS9gXmhplzXO7WDawsL2goeVAmOGl5OFS6k9Ugs6rJ3hY-gXo7hb7AXOOoK11vssBqNDYfPkFBVcKq2tMOk6iEo9V8lCVKiQ7vPYvtgkmqoVpARA5EmUqAfQWIYCf7CFAz0p_MxZGSsEvgsGuLRFEkhQiESjQDM3aNVp7_WoyZix-1G00http://www.plantuml.com/plantuml/svg/NL4zZzGm4EtzAqoNI6ZJKztj7GKD5FS38XFFnHQsPpKUSqJe92eQH8aea3Yn1QBQ7Wf-3U7ZNn1damqabT-Rv_SyBsUH5N7oJjopeN59WpJCk_YWgaZTR5hB9ZrD4QZ1m11uqw2lse0wlQWQT4Z3rSgho40dlDbbFxRiGFxu-hd_zlxNuLN_zjsV_Ul-xkxdbq_znpVzX-_2mJNNZ3NPrd1H2gE2hc_8Ceo0TErio6S7BGGz78H73u6BtuVzu7V_2McWygMGmsS3on4_qYTynOfJ5E9slhUrpfKpk0HddmDrfM1ZGrji4P-LGaDiYWlqMH9BGUYWk4YHqGFDoeT-vx03cAAlc0PMFbOUHdof6EJM4XkjkjLZXYLk9vVpn0PfZi145cPqtZIO0W-gKeXf9Ay9_H8j5irw8l8cClymPKDSbZdoHiLQdyB7oXPjBcXDBaKT1zbXAYlBC_plmRCy3vQzvWv7DlkikUMPHrkdEanSft_Ypo3evDrV)