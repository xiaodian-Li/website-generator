---
title: 关于js方法的单测
date: 2018-05-31 11:47:28
tags: [单测, js]
categories: js
---
基于封装的js方法库，了解了chai.js断言库以及Mocha测试框架，下面我简单介绍记录一下，以方便自己回顾。
# chai.js
chai.js有两种风格的API,分别是BDD风格的expect/should的API，TDD风格的Assert的API，下面主要介绍BDD风格的API  <br><!--more-->
#### 1.expect与should区别
* 初始化断言方式，expect使用构造函数来创建断言对象实例，而should通过为Object.prototype新增方法来实现断言（所以should不支持IE）  
* expect直接指向chai.expect，而should则是chai.should()
```
var chai = require('chai') ,
  expect = chai.expect ,
  should = chai.should()
```
#### 2.工具库用到的相关api
* .not对之后的断言取反
```
expect(foo).to.not.equal('bar')
expect(goodFn).to.not.throw(Error)
expect({ foo: 'baz'}).to.have.property('foo')
  .and.not.equal('bar')
```
* .any在keys断言之前使用any标记（与all相反）
```
expect(foo).to.have.any.keys('bar', 'baz')
```
* .all在keys断言之前使用all标（与any相反）
```
expect(foo).to.have.all.keys('bar', 'baz')
```
* .a(type) / .an(type)  
type：String，被测试的值的类型  
a和an断言即可作为语言链又可作为断言使用
```
// 类型断言
expect('test').to.be.a('string');
expect({ foo: 'bar' }).to.be.an('object');
// es6 overrides
expect({[Symbol.toStringTag]:()=>'foo'}).to.be.a('foo');

// language chain
expect(foo).to.be.an.instanceof(Foo);
```
* .include(value) / contains(value)  
value：Object | String | Number    
include()和contains()即可作为属性类断言前缀语言链又可作为作为判断数组、字符串是否包含某值的断言使用。当作为语言链使用时，常用于key()断言之前
```
expect([1, 2, 3]).to.include(2)
expect('foobar').to.include('bar')
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo')
```
* .ok断言目标为真值
```
expect(1).to.be.ok
```
* .true断言目标为true，注意，这里与ok的区别是不进行类型转换，只能为true才能通过断言
```
expect(true).to.be.true
expect(1)to.not.be.true
```
* .false断言目标为false
* .exist断言目标存在，即非null也非undefined
```
var foo = 'hi',
  bar = null,
  baz

expect(foo).to.exist
expect(bar).to.not.exist
expect(baz).to.not.exist
```

# Mocha测试框架
#### 1.目录内部安装  

安装,先安装这个库
```
git clone https://github.com/ruanyf/mocha-demos.git
```
进入mocha-demos,安装依赖
```
cd mocha-demos
npm install
```
#### 2.全面环境安装  
```
npm install --global 
```
#### 3.测试脚本写法
* 测试脚本与所要测试的源码脚本同名，但是后缀名为.test.js（表示测试）
```
// add.js
function add(x, y) {
  return x + y;
}

module.exports = add;
```
```
// add.test.js
var add = require('./add.js');
var expect = require('chai').expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```
测试脚本里面应该包括一个或多个describe块，每个describe块应该包括一个或多个it块。  

describe块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。  

it块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数。  

#### 4.Mocha的基本用法
* 进入要测试的测试目录
```
mocha add.test.js

  加法函数的测试
    ✓ 1 加 1 应该等于 2

  1 passing (8ms)
  
上面表示1个测试脚本通过测试，耗时8毫秒  
```

* mocha命令后面紧跟测试脚本的路径和文件名，可以指定多个测试脚本
```
mocha file1 file2 file3
```
* mocha默认运行test目录下面的测试脚本，运行test目录里面不需要后接参数
```
mocha
运行test目录下所有脚本
```
* 如果test里面嵌套测试脚本，或者更深层的嵌套测试脚本，只需要执行
```
mocha --recursive
不管多少嵌套测试脚本，都执行
```
#### 5.配置文件mocha.opts
将这三个参数--recursive、--reporter tap、--growl写入test目录下的mocha.opts文件。  
然后执行
```
mocha
等于
mocha --recursive --reporter tap --growl

打开--growl参数，就会将测试结果在桌面显示
打开--reporter参数用来指定测试报告的格式，默认是spec格式，js工具库用的tap格式  
打开--recursive不管多少嵌套测试脚本，都执行
```
如果测试用例不是存放在test子目录，可以在mocha.opts写入以下内容。
```
server-tests
--recursive
```
上面代码指定运行server-tests目录及其子目录之中的测试脚本
#### 6.ES6测试
如果测试脚本是用ES6写的，那么运行测试之前，需要先用Babel转码
```
import add from '../src/add.js';
import chai from 'chai';

let expect = chai.expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```
ES6转码，需要安装Babel。
```
npm install babel-core babel-preset-es2015 --save-dev
```
然后，在项目目录下面，新建一个.babelrc配置文件。
```
{
  "presets": [ "es2015" ]
}
```
最后，使用--compilers参数指定测试脚本的转码器。
```
$ ../node_modules/mocha/bin/mocha --compilers js:babel-core/register
```
上面代码中，--compilers参数后面紧跟一个用冒号分隔的字符串，冒号左边是文件的后缀名，右边是用来处理这一类文件的模块名。  
上面代码表示，运行测试之前，先用babel-core/register模块，处理一下.js文件。由于这里的转码器安装在项目内，所以要使用项目内安装的Mocha；如果转码器安装在全局，就可以使用全局的Mocha。

下面是另外一个例子，使用Mocha测试CoffeeScript脚本。测试之前，先将.coffee文件转成.js文件。
```
$ mocha --compilers coffee:coffee-script/register
```
注意，Babel默认不会对Iterator、Generator、Promise、Map、Set等全局对象，以及一些全局对象的方法（比如Object.assign）转码。如果你想要对这些对象转码，就要安装babel-polyfill。
```
$ npm install babel-polyfill --save
```
然后，在你的脚本头部加上一行。
```
import 'babel-polyfill'
```

> 参考文章：  
http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html  
http://www.chaijs.com/api/bdd/