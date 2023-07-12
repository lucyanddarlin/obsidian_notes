对于前端来说，后端主要是提供 http 接口来传输数据的，而这种数据传输的方式主要有 5 中：
- url param
- query
- form-urlencoded
- form-data
- json

## 了解
### url param
直接将参数写在 url 中
```javascript
http://xxxxx/person/111
```

### query
在 url 中通过 `?` 后面的 `&` 分隔的字符串来传递数据：
``` javascript
http://xxxxx/person?name=lucy&age=18
```

### form-urlencoded
直接用 form 表单提交数据就是这种，它和 query 的区别只是将参数放在了 body 里，`content-type` 指定是 `application/x-www-form-urlencoded`

### from-data
form-data 需要指定 `content-type` 为 `multipart/form-data`，这种方式适合传输文件，而且可以传输多个文件

### json
如果只是传输 json 数据的话，可以指定指定 `content-type` 为 `applicaton/json`

## Nestjs 中的实现
### url params
```js
// http:localhost:3000/person/3000
  @Get(':id')
  urlParam(@Param('id') id: string) {
    return `receive ${id} person`;
  }
```

### query
```js
// http:localhost/person/find?name=lucy&age=19
  @Get('find')
  query(@Query('name') name: string, @Query('age') age: number) {
    return `find name-${name} / age-${age}`;
  }
```

### form-urlencoded / json
使用 `@Body` 装饰器，Nest 会解析请求体，然后注入到 `dto` 中
`dto` 是 data transfer object，就是用于封装传输数据的对象
```js

	// create-person.dto.ts
export class CreatePersonDto {
  name: string;
  age: number;
}

  @Post()
  body(@Body() createPerson: CreatePersonDto) {
    return `receive peron: ${JSON.stringify(createPerson)}`;
  }
```

### from-data
Nest 解析 form data 使用 `FileInterceptor` 的拦截器，用 `@UseInterceptors` 装饰器启用，然后通过 `@UploadFiles` 来取。
对于非文件数据，同样是通过 `@Body` 来取
```js
  @Post('file')
  @UseInterceptors(AnyFilesInterceptor({ dest: 'uploads/' }))
  body2(
    @Body() createPerson: CreatePersonDto,
    @UploadedFiles() files: Array<Express.Multer.File>,
  ) {
    console.log(files);
    return `receive peron: ${JSON.stringify(createPerson)}`;
  }
```
