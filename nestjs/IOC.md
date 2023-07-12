
后端系统中，会有很多对象。这些对象有着错综复杂的关系。使用之前要理清他们的依赖关系，哪个先创建哪个后创建。非常麻烦

## 什么是 IOC
之前手动创建和组装对象十分麻烦，那能不能在 class 上声明依赖了什么呢，然后让工具去分析我声明的依赖关系，根据先后顺序自动把对象创建好，然后组装起来呢？
这就是 IOC 的实现思路。
它有一个放对象的容器，程序初始化的时候会扫描 class 上声明的依赖关系，然后把这些 class 都 new 一个实例放到容器里

创建对象的时候，还会把它们依赖的对象注入进去。这就完成了自动的对象创建和组装
这种依赖注入的方式叫做 `Dependency Injection` ，简称 DI

从主动创建依赖到被动等待依赖注入，这就是 `Inverse of Control` ，反转控制

在 class 上声明依赖的方式，大家都选择了装饰器的方式（在 Java 里这种语法叫做注解）
```js
import { Injectable } from '@nestjs/common';

@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```
