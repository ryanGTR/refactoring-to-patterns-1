# 将装饰功能搬移到 Decorator

- 实现

  - 将装饰代码搬移到 Decorator 

- 动机

  - 添加新功能时，会使原有类的核心职责或主要行为变复杂，而这些新东西只在特定情况下才执行

- 优点

  - 把装饰功能从类中搬移去除，从而简化了类
  - 有效地把类的核心职责和装饰功能区分开来
  - 可以去除几个相关类中重复的装饰逻辑

- 缺点

  - 改变了被装饰对象的对象类型
  - 会使代码变得更难理解和调试
  - 当 Decorator 组合产生负面影响的时候，会增加设计的复杂度

- Decorator 和 Strategy 的对比

  - 相同点

    - 都可以去除与特殊情况或选择性行为相关联的条件逻辑
    - 都通过把这些行为从原来的类搬移到一个或多个新类中达到这一目的

  - 不同点

    - Decorator

      - 把自己包装在一个对象之外

    - Strategy

      - 用在一个对象当中

  - 选择用哪一个？

    - Strategy

      - 实例可共享
      - 可以随意定义自己的接口
      - 使用 Strategy 必须知道他们的存在、了解他们
      - 对包含很多数据或实现很多公共方法的类使用一个或多个 Strategy 很常见

    - Decorator

      - 不能共享实例
      - 接口必须与它所装饰的类的接口一致
      - 可以透明地为多个不同的类添加行为
      - 对包含很多数据或实现很多公共方法的类使用 Decorator 会变得很笨重

- 做法

  - 确定或创建包装类型、接口或类，它声明了客户代码需要的被装饰类的公共方法
  - 找到为被修饰类添加装饰功能的条件逻辑，并应用用多态替换条件式重构去除这些逻辑
  - 步骤（2）产生了被修饰类的一个或多个子类。应用用委托替换集成重构把这些子类转换成委托类

    - 使每个委托类都实现包装类型
    - 把委托类的委托字段的类型声明为包装类型
    - 决定装饰代码在委托类调用委托之前还是之后执行