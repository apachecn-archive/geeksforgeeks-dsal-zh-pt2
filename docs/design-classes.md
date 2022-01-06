# 设计类

> 原文:[https://www.geeksforgeeks.org/design-classes/](https://www.geeksforgeeks.org/design-classes/)

[需求模型](https://www.geeksforgeeks.org/elements-of-the-requirements-model/)定义了一组分析类。每一个都描述了问题域的一些元素，集中在问题的一个可见的方面。分析类的抽象程度比较高。设计类集合细化了分析类，并提供了设计细节，使类能够执行支持业务解决方案的软件基础设施。

### 类型:

有 5 种不同类型的设计类代表了可以开发的设计架构的不同层:

1.  **The user interface class** defines the abstraction necessary for human-computer interaction. In some cases, human-computer interaction occurs in the context of metaphor, and the design class of the interface may be the visible representation of metaphor elements.
2.  **Business domain class** is usually a refinement of the previously defined analysis class. This class identifies the attributes needed to implement some elements of the business domain.
3.  **Process class implementation** The business domain class needs to be managed by the subordinate business concerns.
4.  **Persistent class** represents data storage that will persist after software execution.
5.  **The system class realizes** the software management and control function, which allows the system to operate and communicate with the outside world in its computing environment.

随着体系结构的形成，随着每个分析类转换成两个设计表示，抽象级别降低了。也就是说，分析类使用业务领域的行话来表示数据对象。设计类提供了更多的技术细节作为实现指南。

**阿洛**和**纽斯塔德**建议对每个设计类进行审查，以确保“格式良好”。它们定义了良好设计类的四个特征:

### 特征:

1.  **完整和充分:**一个设计类应该是能够合理预期该类存在的所有属性和方法的完整封装。例如，为视频编辑软件定义的类**场景**只有包含所有可以愉快地与视频场景的创建相关联的属性和方法时才是完整的。充分确保设计类只包含那些足以实现类意图的方法，不多也不少。
2.  **原始性:**与设计类相关联方法应该专注于为类完成一项服务。一旦用方法实现了服务，类就不应该提供另一种方法来完成同样的事情。例如，视频编辑软件的类**视频剪辑**可能有属性*起点*和*终点*来指定剪辑的起点和终点。
3.  **高内聚/强>一个内聚设计类有一个小的、集中的权限集，并且一心一意地应用属性和方法来实现那些职责。例如，类**视频剪辑**可能包含一组编辑视频剪辑的方法。只要每种方法只关注与视频剪辑相关的属性，就能保持凝聚力。**
4.  ****低耦合:**在设计模型内部，设计类之间有必要聚在一起。然而，聚会应该保持在可接受的最低限度。如果设计模型是高度耦合的，那么系统很难实现测试和长期维护。一般来说，子系统内的设计类应该只有有限的其他类的知识。这个限制叫做德米特里定律，建议方法应该只向相邻类中的方法发送消息。**