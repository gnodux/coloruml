#基于PlantUML 的4色 领域模型建模

## 关于PlantUML

PlantUML是一个开源项目，支持快速绘制：

- 时序图
- 用例图
- 类图
- 活动图 (旧版语法在此处)
- 组件图
- 状态图
- 对象图
- 部署图 
- 定时图 

同时还支持以下非UML图:

- 线框图形界面
- 架构图
- 规范和描述语言 (SDL)
- Ditaa diagram
- 甘特图 
- 思维导图 
- Work Breakdown Structure diagram 
- 以 AsciiMath 或 JLaTeXMath 符号的数学公式
- Entity Relationship diagram

具体语法可以参考：[PlantUML](http://plantuml.com)

## 关于4色领域模型建模

4色领域模型的概念来自 [Java Modeling In Color With UML](https://book.douban.com/subject/1440291/) 


_Peter Coad提出的几类基本元模型对于实际进行建模工作有着非比寻常的指导价值——当大多数人在分析业务领域模型时，Peter Coad在分析业务领域的元模型，其“鬼才”由此可见一斑。至于“带颜色的UML”，无非是对元模型的一种直观描述而已。对于面向对象（而非面向用例）的企业应用业务建模，这本“小书”便是首屈一指的最佳实践指南._

在这本小书里，ArcheType 被分为：

- Moment-Interval
- Role
- Description
- "Party,Place, or Thing"

4种类型。通过对对象的分类，快速抓住关键业务控制点。

领域模型建模的相关概念及链接:

* [https://www.infoq.cn/article/xh-four-color-modeling](https://www.infoq.cn/article/xh-four-color-modeling)
* [从“四色建模法”到“限界纸笔建模法”](https://insights.thoughtworks.cn/paper-pen-modeling/)
* [谈谈领域建模](http://fanyilun.me/2018/04/08/%E8%B0%88%E8%B0%88%E9%A2%86%E5%9F%9F%E5%BB%BA%E6%A8%A1/)

## 关于color uml

这个项目是在PlantUML的基础上的定制，支持快速绘制领域模型图

## Getting start

在绘制领域模型图的时候，直接引用:

```
!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
```

例如一个简单的示例:

[Book Store](samples/bookstore.puml)

```csharp
@startuml

!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml

moment(Order)
moment(Bill)
moment(Delivery)
thing(Book)
role(Customer)

Order contains(Bill)
Order contains(Delivery)
Order has(Book)
Customer has(Order)
@enduml
```
![Book Store](http://www.plantuml.com/plantuml/png/NSwxJiKm30RWFKznsDgbsPcE2ZlF41AhYV2bScmkRuzQGeSp_h_bpxvtIsfE6C9JuunUu5RDzluSewQlPMjM_TqxQ1OsO5koKDnOYd_7B2ZgX95IDz0hB_i9aX2mJMzQGEV_j3R4Axm2ja_GdpbORRnDgyZ775GGfXVl9dGiXXEu7VTJupw4X_AIng2cFhG_Q5JZbpjmSS9V "Book store") 