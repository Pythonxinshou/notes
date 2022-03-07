接口：

GET

http://apis.juhe.cn/mobile/get?key=ffe950dd3e85ee36de34b33575d1e177&phone=15874198829

POST

http://apis.juhe.cn/simpleWeather/query

{"city":"南京","key":"371e78e1c2d2eeabb361294723857e8d"}

### 一、断言常见方法

进入**Tests**的Tab页里可以通过SNIPPETS下方点击快捷添加断言代码

Response body: Contains string	验证响应数据是否包含某一字符串

```js
pm.test("验证响应数据是否包含某一字符串", function () {
  pm.expect(pm.response.text()).to.include("Return Successd!");
});
```

Response body: Is equal to a string	验证响应数据是否等于某一字符串

```js
pm.test("验证响应数据是否等于某一字符串", function () {
    pm.response.to.have.body({
    "resultcode": "200",
    "reason": "Return Successd!",
    "result": {
        "province": "湖南",
        "city": "长沙",
        "areacode": "0731",
        "zip": "410000",
        "company": "移动",
        "card": ""
    },
    "error_code": 0
});
});
```

Response body: JSON value check	验证响应的JSON数据中某一个值

```js
pm.test("验证响应的JSON数据中某一个值", function () {
    var jsonData = pm.response.json();
    pm.expect(jsonData.resultcode).to.eql("200");
});
```

Status code: Code is 200	验证状态码是否为200

```js
pm.test("验证状态码是否为200", function () {
    pm.response.to.have.status(200);
});
```

Response headers: Content-Type header check	校验响应头是否包含某头部信息(key)

```js
pm.test("校验响应头是否包含某头部信息(key)", function () {
    pm.response.to.have.header("Date");
});
```

### 二、设置变量

进入**Pre-request Script**的Tab页

在请求前会执行的脚本代码块，注：环境与全局变量需要执行一次才能添加到环境中，被其他的接口调用

1. 本地变量：作用于当前请求

   pre-request script

   ```js
   pm.variables.set("变量名", "参数值");
   ```

   调用变量：{{变量名}}

2. 环境变量：作用于当前环境下的所有请求

   老版点击齿轮添加环境-添加环境变量，新版点击眼睛-Environment Add添加环境变量

   ```js
   pm.environment.set("variable_key", "variable_value");
   ```

   调用变量：{{变量名}}

3. 全局变量：作用于所有请求

   ```js
   pm.globals.set("variable_key", "variable_value");
   ```

   老版点击齿轮-点击Globals添加全局变量，新版点击眼睛-Globals Add添加全局变量

4. 数据变量：通过读取外部数据文件进行传值

   文档参数化：postman支持的文档参数化

   - txt
   - csv
   - json

   在Collections中对接口完成分类后，老版点击包名旁的三角形，点击Run，新版点击。。。下拉选择Run Collection

   勾选需要的接口，lterations是设置循环次数，Delay是设置延迟执行多少ms，Data选择数据文件

   ```
   weatherkey,city,phonekey,phone
   371e78e1c2d2eeabb361294723857e8d,北京,ffe950dd3e85ee36de34b33575d1e177,15348319213
   371e78e1c2d2eeabb361294723857e8d,上海,ffe950dd3e85ee36de34b33575d1e177,15348319214
   371e78e1c2d2eeabb361294723857e8d,深圳,ffe950dd3e85ee36de34b33575d1e177,15348319215
   ```

   注意文件格式，第一行为变量名称，需要跟接口中的变量名保持一致，如：

   ```js
   http://apis.juhe.cn/mobile/get?key={{phonekey}}&phone={{phone}}
   ```

   导入文件后，可能会提示无法识别数据格式，手动选择text/csv或其它对应的格式，可点击Preview预览文件数据与变量是否对应且正确，最后点击Run Data开始执行文件

### 三、关联接口

一个接口的结果作为另一个接口的入参

进入**Tests**的Tab页

```js
var jsondata=pm.reponse.json()//定义变量jsondata获取json格式的返回结果
var city=jsondata.result["city"]//定义变量提取出需要的city对应的值（长沙）
pm.environment.set("citydata1",city)//添加环境变量citydata1并给它赋值
```

接口执行完后会在环境变量里添加变量名为"citydata1"的变量，后续接口调用可以{{citydata1}}

