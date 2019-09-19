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

!include https://raw.githubusercontent.com/gnodux/coloruml/master/coloruml.puml
'
'!include ../coloruml.puml
left_to_right

moment(Order)
moment(Bill)
moment(Delivery)
thing(Book)
desc(Comments)
role(Customer)
thing(Employee)
thing(Author)
role(Courier)
role(Accounting)

Courier from(Employee)
Accounting from(Employee)

Book contains(Comments)
Book has(Author)
Order contains(Bill)
Order contains(Delivery)
Order has(Book)
Bill has(Accounting)
Delivery has(Courier)
Customer has(Order)

@enduml
```
![Book Store](http://www.plantuml.com/plantuml/png/NP2zLiCm38LtFqMPcYp9pjGVc7c4dk2eiG-IbIDBGDyUJ7426Q_kPrdt7h8EeaRe7cBoQ2FiWkgS7_jUXezkYXhirJA8vwIGjFDC_PHujC_UCx8OOKz3Lf15TtFPjtVxPMNNRKo4grwKBnAdeCuH4oHjNcG4QQiwHSH5F076Tv1RwpJ4D3KdvhVMZP1zSsOgI6wTC49pjgnC89LyfXdv1b3rqJImL9XD8bHrz9ujwJVLElThxQx2z6V9ocmTLsxQbPw6cF9wrdqUXhny_PDp9KlGxN09N8to_Xwwu4N-ExVYnLXJrIxAjBPxW3GQuHS0 "Book store")

## IntelliJ IDEA 集成


* 在JetBrains 下载IntelliJ IDEA [Download IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
* 安装Plugins: PlantUML Integration / PlantUML Syntax Checker

