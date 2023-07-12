provider 一般都是用 `@injectable` 修饰的 class
```js
import { Injectable } from '@nestjs/common';
  
@Injectable()
export class AppService {
  getHello(): string {
    return 'Hello World!';
  }
}
```
在 `Module` 的 `providers` 中声明：
```js
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { PersonModule } from './person/person.module';

@Module({
  imports: [PersonModule],
  controllers: [AppController],
  providers: [AppService],
})
export class AppModule {}
```
以下是 `providers` 的完整写法:
```js
import { Module } from '@nestjs/common';
import { AppController } from './app.controller';
import { AppService } from './app.service';
import { PersonModule } from './person/person.module';

@Module({
  imports: [PersonModule],
  controllers: [AppController],
  providers: [{provide: AppService, useClass: AppService}],
})
export class AppModule {}
```
通过 `providers` 指定注入的 `token`，通过 `useClass` 指定注入的对象的类，Nest 会自动会它实例化再注入, 可以通过构造函数注入，也可以通过属性注入:
```js
import { Controller, Get, Inject } from '@nestjs/common';

import { AppService } from './app.service';

@Controller()
export class AppController {
  // 构造函数注入
  // constructor(private readonly appService: AppService) {}

  // 属性注入
  @Inject(AppService)
  private readonly appService: AppService;

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```
同时，`providers` 中也可以将字符串作为 token，注入的时候也要标明对应的字符串 token 即可：
```js
// app.module.ts
...
@Module({
  imports: [PersonModule],
  controllers: [AppController],
  providers: [{provide: 'app_service', useClass: AppService}],
})
...

// app.controller.ts
...
@Controller()
export class AppController {
...
  // 属性注入
  @Inject('app_service')
  private readonly appService: AppService;

  @Get()
  getHello(): string {
    return this.appService.getHello();
  }
}
```

除了指定 class 外，还可以直接指定一个值，让 IOC 注入：
```js
// app.module.ts
...
@Module({
  imports: [PersonModule],
  controllers: [AppController],
  providers: [
	  ..., 
	 { 
		provide: 'person', 
		useValue: {name: 'aaa', age: 20}
	 }],
})
...

// app.controller.ts
...
@Controller()
export class AppController {
...
  // 属性注入
  @Inject('person')
  private readonly person: {name:string, age: number};
...
```

`provider` 的值可能是动态产生的，使用 `useFactory` 来动态创建一个对象：
```js
// app.module.ts
{
	provide: 'person',
	useFactory() {
		return {
			name: 'lucy',
			age: 18
		}
	}
}
```
同时，useFactory 也支持参数的注入：
```js
{
      provide: 'person3',
      useFactory(person: { name: string }, appService: AppService) {
        return {
          name: person.name,
          desc: appService.getHello()
        }
      },
      inject: ['person', AppService]
}
```

在调用 useFactory 方法的时候，Nest 就会注入这两个对象。