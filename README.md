[原文: https://github.com/airbnb/javascript](https://github.com/airbnb/javascript)

注：删除和修改了部分规范       
   如果你是新手请仔细阅读整篇文章，如果你是老手至少需要阅读[命名约定](#naming-conventions), [注释](#comments), [空白](#whitespace) 和 [换行](#line-break)


# JavaScript规范

## <a name='TOC'>内容列表</a>

  1. [命名约定](#naming-conventions)
  1. [注释](#comments)
  1. [空白](#whitespace)
  1. [换行](#line-break)
  1. [类型](#types)
  1. [对象](#objects)
  1. [数组](#arrays)
  1. [字符串](#strings)
  1. [函数](#functions)
  1. [属性](#properties)
  1. [变量](#variables)
  1. [条件表达式和等号](#conditionals)
  1. [块](#blocks)
  1. [逗号](#commas)
  1. [分号](#semicolons)
  1. [类型转换](#type-coercion)
  1. [存取器](#accessors)
  1. [构造器](#constructors)
  1. [事件](#events)
  1. [模块](#modules)
  1. [jQuery](#jquery)
  1. [JavaScript风格指南](#guide-guide)


## <a name='naming-conventions'>命名约定</a>

  - 避免单个字符名，让你的变量名有描述意义。

      ```json
      // bad
      function q() {
        // ...stuff...
      }

      // good
      function query() {
        // ..stuff..
      }
      ```

  - 当命名对象、函数和实例时使用驼峰命名规则。 除了类名和类的构造函数，其他变量和函数首字母要小写。 

      ```json
      // bad
      var OBJEcttsssss = {};
      var this_is_my_object = {};
      var this-is-my-object = {};
      function c() {};
      var u = new user({
        name: 'Bob Parr'
      });

      // good
      var thisIsMyObject = {};
      function thisIsMyFunction() {};
      var user = new User({
        name: 'Bob Parr'
      });
      ```

  - 当命名构造函数或类时使用驼峰式大写

      ```json
      // bad
      function user(options) {
        this.name = options.name;
      }

      var bad = new user({
        name: 'nope'
      });

      // good
      function User(options) {
        this.name = options.name;
      }

      var good = new User({
        name: 'yup'
      });
      ```

  - 变量名应该以名词开始，函数命应该以动词开始

      ```json
      // Good
      var count = 10;
      var myName = "Nicholas";
      var found = true;

      // Bad: Easily confused with functions
      var getCount = 10;
      var isFound = true;

      // Good
      function getName() {
          return myName;
      }

      // Bad: Easily confused with variable
      function theName() {
          return myName;
      }
      ```

      函数命中惯用动词     

      |      动词      |        含义       |          
      | ------------- | ----------------- |        
      | can |  Function returns a boolean |         
      | has |  Function returns a boolean |       
      | is  |  Function returns a boolean |       
      | get |  Function returns a nonboolean |      
      | set |  Function is used to save a value |                  

  - 常量名应该大写，单词之间用下划线`_`隔开

      ```json
      var MAX_COUNT = 10;
      var URL = "http://www.nczonline.net/";
      ```

  - 当保存对 `this` 的引用时使用 `_this`.

      ```json
      // bad
      function() {
        var self = this;
        return function() {
          console.log(self);
        };
      }

      // bad
      function() {
        var that = this;
        return function() {
          console.log(that);
        };
      }

      // good
      function() {
        var _this = this;
        return function() {
          console.log(_this);
        };
      }
      ```

    **[[⬆]](#TOC)**


## <a name='comments'>注释</a>

  - 使用 `/** ... */` 进行多行注释，包括描述，指定类型以及参数值和返回值

      ```json
      // bad
      // make() returns a new element
      // based on the passed in tag name
      //
      // @param <String> tag
      // @return <Element> element
      function make(tag) {

        // ...stuff...

        return element;
      }

      // good
      /**
       * make() returns a new element
       * based on the passed in tag name
       *
       * @param <String> tag
       * @return <Element> element
       */
      function make(tag) {

        // ...stuff...

        return element;
      }
      ```

  - 使用 `//` 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.

      ```json
      // bad
      var active = true;  // is current tab

      // good
      // is current tab
      var active = true;

      // bad
      function getType() {
        console.log('fetching type...');
        // set the default type to 'no type'
        var type = this._type || 'no type';

        return type;
      }

      // good
      function getType() {
        console.log('fetching type...');

        // set the default type to 'no type'
        var type = this._type || 'no type';

        return type;
      }
      ```

  - 如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话需要在你的注释前面加上 `FIXME` 或 `TODO` 帮助其他人迅速理解

      ```json
      function Calculator() {

        // FIXME: shouldn't use a global here
        total = 0;

        return this;
      }
      ```

      ```json
      function Calculator() {

        // TODO: total should be configurable by an options param
        this.total = 0;

        return this;
      }
    ```

    **[[⬆]](#TOC)**


## <a name='whitespace'>空白</a>

  - 将tab设为4个空格

      ```json
      // bad
      function() {
      ∙∙var name;
      }

      // bad
      function() {
      ∙var name;
      }

      // good
      function() {
      ∙∙∙∙var name;
      }
      ```
    - 大括号前放一个空格

      ```json
      // bad
      function test(){
        console.log('test');
      }

      // good
      function test() {
        console.log('test');
      }

      // bad
      dog.set('attr',{
        age: '1 year',
        breed: 'Bernese Mountain Dog'
      });

      // good
      dog.set('attr', {
        age: '1 year',
        breed: 'Bernese Mountain Dog'
      });
      ```

  - 在做长方法链时使用缩进.

      ```json
      // bad
      $('#items').find('.selected').highlight().end().find('.open').updateCount();

      // good
      $('#items')
        .find('.selected')
          .highlight()
          .end()
        .find('.open')
          .updateCount();

      // bad
      var leds = stage.selectAll('.led').data(data).enter().append('svg:svg').class('led', true)
          .attr('width',  (radius + margin) * 2).append('svg:g')
          .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
          .call(tron.led);

      // good
      var leds = stage.selectAll('.led')
          .data(data)
        .enter().append('svg:svg')
          .class('led', true)
          .attr('width',  (radius + margin) * 2)
        .append('svg:g')
          .attr('transform', 'translate(' + (radius + margin) + ',' + (radius + margin) + ')')
          .call(tron.led);
      ```

    **[[⬆]](#TOC)**

## <a name='line-break'>换行</a>

  - 一行代码应该不超过80个字符，否则阅读会很不方便
  - 超过80个字符的代码应该换行，此时换行要使用两倍缩进（8个空格）

    ```json
    // Good: Break after operator, following line indented two levels
    callAFunction(document, element, window, "some string value", true, 123,
            navigator);

    // Bad: Following line indented only one level
    callAFunction(document, element, window, "some string value", true, 123,
        navigator);

    // Bad: Break before operator
    callAFunction(document, element, window, "some string value", true, 123
            , navigator);
    ```

  - 特殊情况，给变量赋值时换行后的变量应该对齐上一个行的第一个变量，列如：

    ```json
    var result = something + anotherThing + yetAnotherThing + somethingElse +
                 anotherSomethingElse;
    ```

    **[[⬆]](#TOC)**


## <a name='types'>类型</a>

  - **原始值**: 相当于传值

    + `string`
    + `number`
    + `boolean`
    + `null`
    + `undefined`

    ```json
    var foo = 1,
        bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```
  - **复杂类型**: 相当于传引用

    + `object`
    + `array`
    + `function`

    ```json
    var foo = [1, 2],
        bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

    **[[⬆]](#TOC)**

## <a name='objects'>对象</a>

  - 使用字面值创建对象

    ```json
    // bad
    var item = new Object();

    // good
    var item = {};
    ```

  - 不要使用保留字 [reserved words](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words) 作为键

    ```json
    // bad
    var superman = {
      class: 'superhero',
      default: { clark: 'kent' },
      private: true
    };

    // good
    var superman = {
      klass: 'superhero',
      defaults: { clark: 'kent' },
      hidden: true
    };
    ```
    **[[⬆]](#TOC)**

## <a name='arrays'>数组</a>

  - 使用字面值创建数组

    ```json
    // bad
    var items = new Array();

    // good
    var items = [];
    ```

  - 如果你不知道数组的长度，使用push

    ```json    

    var someStack = [];

    // bad
    someStack[someStack.length] = 'abracadabra';

    // good
    someStack.push('abracadabra');
    ```

  - 当你需要拷贝数组时使用slice. [jsPerf](http://jsperf.com/converting-arguments-to-an-array/7)

    ```json
    var len = items.length,
        itemsCopy = [],
        i;

    // bad
    for (i = 0; i < len; i++) {
      itemsCopy[i] = items[i];
    }

    // good
    itemsCopy = items.slice();
    ```

  - 使用slice将类数组的对象转成数组.

    ```json
    function trigger() {
      var args = Array.prototype.slice.call(arguments);
      ...
    }
    ```

    **[[⬆]](#TOC)**


## <a name='strings'>字符串</a>

  - 对字符串使用单引号 `''`

    ```json
    // bad
    var name = "Bob Parr";

    // good
    var name = 'Bob Parr';

    // bad
    var fullName = "Bob " + this.lastName;

    // good
    var fullName = 'Bob ' + this.lastName;
    ```

  - 超过80个字符的字符串应该使用字符串连接换行
  - 注: 如果过度使用，长字符串连接可能会对性能有影响. [jsPerf](http://jsperf.com/ya-string-concat) & [Discussion](https://github.com/airbnb/javascript/issues/40)

    ```json
    // bad
    var errorMessage = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.';

    // bad
    var errorMessage = 'This is a super long error that \
    was thrown because of Batman. \
    When you stop to think about \
    how Batman had anything to do \
    with this, you would get nowhere \
    fast.';


    // good
    var errorMessage = 'This is a super long error that ' +
      'was thrown because of Batman.' +
      'When you stop to think about ' +
      'how Batman had anything to do ' +
      'with this, you would get nowhere ' +
      'fast.';
    ```

  - 编程时使用join而不是字符串连接来构建字符串，特别是IE: [jsPerf](http://jsperf.com/string-vs-array-concat/2).

    ```json
    var items,
        messages,
        length, i;

    messages = [{
        state: 'success',
        message: 'This one worked.'
    },{
        state: 'success',
        message: 'This one worked as well.'
    },{
        state: 'error',
        message: 'This one did not work.'
    }];

    length = messages.length;

    // bad
    function inbox(messages) {
      items = '<ul>';

      for (i = 0; i < length; i++) {
        items += '<li>' + messages[i].message + '</li>';
      }

      return items + '</ul>';
    }

    // good
    function inbox(messages) {
      items = [];

      for (i = 0; i < length; i++) {
        items[i] = messages[i].message;
      }

      return '<ul><li>' + items.join('</li><li>') + '</li></ul>';
    }
    ```

    **[[⬆]](#TOC)**


## <a name='functions'>函数</a>

  - 函数表达式:

    ```json
    // 匿名函数表达式
    var anonymous = function() {
      return true;
    };

    // 有名函数表达式
    var named = function named() {
      return true;
    };

    // 立即调用函数表达式
    (function() {
      console.log('Welcome to the Internet. Please follow me.');
    })();
    ```

  - 绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同。
  - **注:** ECMA-262定义把`块`定义为一组语句，函数声明不是一个语句。[阅读ECMA-262对这个问题的说明](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97).

    ```json
    // bad
    if (currentUser) {
      function test() {
        console.log('Nope.');
      }
    }

    // good
    if (currentUser) {
      var test = function test() {
        console.log('Yup.');
      };
    }
    ```

  - 绝对不要把参数命名为 `arguments`, 这将会逾越函数作用域内传过来的 `arguments` 对象.

    ```json
    // bad
    function nope(name, options, arguments) {
      // ...stuff...
    }

    // good
    function yup(name, options, args) {
      // ...stuff...
    }
    ```

    **[[⬆]](#TOC)**


## <a name='properties'>属性</a>

  - 当使用变量访问属性时使用中括号.

    ```json
    var luke = {
      jedi: true,
      age: 28
    };

    function getProp(prop) {
      return luke[prop];
    }

    var isJedi = getProp('jedi');
    ```

    **[[⬆]](#TOC)**


## <a name='variables'>变量</a>

  - 总是使用 `var` 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。

    ```json
    // bad
    superPower = new SuperPower();

    // good
    var superPower = new SuperPower();
    ```

  - 使用一个 `var` 以及新行声明多个变量，缩进4个空格。

    ```json
    // bad
    var items = getItems();
    var goSportsTeam = true;
    var dragonball = 'z';

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball = 'z';
    ```

  - 最后再声明未赋值的变量，当你想引用之前已赋值变量的时候很有用。

    ```json
    // bad
    var i, len, dragonball,
        items = getItems(),
        goSportsTeam = true;

    // bad
    var i, items = getItems(),
        dragonball,
        goSportsTeam = true,
        len;

    // good
    var items = getItems(),
        goSportsTeam = true,
        dragonball,
        length,
        i;
    ```

  - 在作用域顶部声明变量，避免变量声明和赋值引起的相关问题。

    ```json
    // bad
    function() {
      test();
      console.log('doing stuff..');

      //..other stuff..

      var name = getName();

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // good
    function() {
      var name = getName();

      test();
      console.log('doing stuff..');

      //..other stuff..

      if (name === 'test') {
        return false;
      }

      return name;
    }

    // bad
    function() {
      var name = getName();

      if (!arguments.length) {
        return false;
      }

      return true;
    }

    // good
    function() {
      if (!arguments.length) {
        return false;
      }

      var name = getName();

      return true;
    }
    ```

    **[[⬆]](#TOC)**


## <a name='conditionals'>条件表达式和等号</a>

  - 适当使用 `===` 和 `!==` 以及 `==` 和 `!=`.
  - 条件表达式的强制类型转换遵循以下规则：

    + **对象** 被计算为 **true**
    + **Undefined** 被计算为 **false**
    + **Null** 被计算为 **false**
    + **布尔值** 被计算为 **布尔的值**
    + **数字** 如果是 **+0, -0, or NaN** 被计算为 **false** , 否则为 **true**
    + **字符串** 如果是空字符串 `''` 则被计算为 **false**, 否则为 **true**

    ```json
    if ([0]) {
      // true
      // An array is an object, objects evaluate to true
    }
    ```

  - 使用快捷方式.

    ```json
    // bad
    if (name !== '') {
      // ...stuff...
    }

    // good
    if (name) {
      // ...stuff...
    }

    // bad
    if (collection.length > 0) {
      // ...stuff...
    }

    // good
    if (collection.length) {
      // ...stuff...
    }
    ```

  - 阅读 [Truth Equality and JavaScript](http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108) 了解更多

    **[[⬆]](#TOC)**


## <a name='blocks'>块</a>

  - 给所有多行的块使用大括号

    ```json
    // bad
    if (test)
      return false;

    // good
    if (test) return false;

    // good
    if (test) {
      return false;
    }

    // bad
    function() { return false; }

    // good
    function() {
      return false;
    }
    ```

    **[[⬆]](#TOC)**


## <a name='commas'>逗号</a>

  - 不要将逗号放前面

    ```json
    // bad
    var once
      , upon
      , aTime;

    // good
    var once,
        upon,
        aTime;

    // bad
    var hero = {
        firstName: 'Bob'
      , lastName: 'Parr'
      , heroName: 'Mr. Incredible'
      , superPower: 'strength'
    };

    // good
    var hero = {
      firstName: 'Bob',
      lastName: 'Parr',
      heroName: 'Mr. Incredible',
      superPower: 'strength'
    };
    ```

  - 不要加多余的逗号，这可能会在IE下引起错误，同时如果多一个逗号某些ES3的实现会计算多数组的长度。

    ```json
    // bad
    var hero = {
      firstName: 'Kevin',
      lastName: 'Flynn',
    };

    var heroes = [
      'Batman',
      'Superman',
    ];

    // good
    var hero = {
      firstName: 'Kevin',
      lastName: 'Flynn'
    };

    var heroes = [
      'Batman',
      'Superman'
    ];
    ```

    **[[⬆]](#TOC)**


## <a name='semicolons'>分号</a>

  - 语句结束一定要加分号

    ```json
    // bad
    (function() {
      var name = 'Skywalker'
      return name
    })()

    // good
    (function() {
      var name = 'Skywalker';
      return name;
    })();

    // good
    ;(function() {
      var name = 'Skywalker';
      return name;
    })();
    ```

    **[[⬆]](#TOC)**


## <a name='type-coercion'>类型转换</a>

  - 在语句的开始执行类型转换.
  - 字符串:

    ```json
    //  => this.reviewScore = 9;

    // bad
    var totalScore = this.reviewScore + '';

    // good
    var totalScore = '' + this.reviewScore;

    // bad
    var totalScore = '' + this.reviewScore + ' total score';

    // good
    var totalScore = this.reviewScore + ' total score';
    ```

  - 对数字使用 `parseInt` 并且总是带上类型转换的基数.

    ```json
    var inputValue = '4';

    // bad
    var val = new Number(inputValue);

    // bad
    var val = +inputValue;

    // bad
    var val = inputValue >> 0;

    // bad
    var val = parseInt(inputValue);

    // good
    var val = Number(inputValue);

    // good
    var val = parseInt(inputValue, 10);

    // good
    /**
     * parseInt was the reason my code was slow.
     * Bitshifting the String to coerce it to a
     * Number made it a lot faster.
     */
    var val = inputValue >> 0;
    ```

  - 布尔值:

    ```json
    var age = 0;

    // bad
    var hasAge = new Boolean(age);

    // good
    var hasAge = Boolean(age);

    // good
    var hasAge = !!age;
    ```

    **[[⬆]](#TOC)**


## <a name='accessors'>存取器</a>

  - 属性的存取器函数不是必需的
  - 如果你确实有存取器函数的话使用getVal() 和 setVal('hello')

    ```json
    // bad
    dragon.age();

    // good
    dragon.getAge();

    // bad
    dragon.age(25);

    // good
    dragon.setAge(25);
    ```

  - 如果属性是布尔值，使用isVal() 或 hasVal()

    ```json
    // bad
    if (!dragon.age()) {
      return false;
    }

    // good
    if (!dragon.hasAge()) {
      return false;
    }
    ```

  - 可以创建get()和set()函数，但是要保持一致

    ```json
    function Jedi(options) {
      options || (options = {});
      var lightsaber = options.lightsaber || 'blue';
      this.set('lightsaber', lightsaber);
    }

    Jedi.prototype.set = function(key, val) {
      this[key] = val;
    };

    Jedi.prototype.get = function(key) {
      return this[key];
    };
    ```

    **[[⬆]](#TOC)**


## <a name='constructors'>构造器</a>

  - 给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题。

    ```json
    function Jedi() {
      console.log('new jedi');
    }

    // bad
    Jedi.prototype = {
      fight: function fight() {
        console.log('fighting');
      },

      block: function block() {
        console.log('blocking');
      }
    };

    // good
    Jedi.prototype.fight = function fight() {
      console.log('fighting');
    };

    Jedi.prototype.block = function block() {
      console.log('blocking');
    };
    ```

  - 方法可以返回 `this` 帮助方法可链。

    ```json
    // bad
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return true;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
    };

    var luke = new Jedi();
    luke.jump(); // => true
    luke.setHeight(20) // => undefined

    // good
    Jedi.prototype.jump = function() {
      this.jumping = true;
      return this;
    };

    Jedi.prototype.setHeight = function(height) {
      this.height = height;
      return this;
    };

    var luke = new Jedi();

    luke.jump()
      .setHeight(20);
    ```


  - 可以写一个自定义的toString()方法，但是确保它工作正常并且不会有副作用。

    ```json
    function Jedi(options) {
      options || (options = {});
      this.name = options.name || 'no name';
    }

    Jedi.prototype.getName = function getName() {
      return this.name;
    };

    Jedi.prototype.toString = function toString() {
      return 'Jedi - ' + this.getName();
    };
    ```

    **[[⬆]](#TOC)**


## <a name='events'>事件</a>

  - 当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里而不用找出并更新那个事件的事件处理器

    ```js
    // bad
    $(this).trigger('listingUpdated', listing.id);

    ...

    $(this).on('listingUpdated', function(e, listingId) {
      // do something with listingId
    });
    ```

    更好:

    ```js
    // good
    $(this).trigger('listingUpdated', { listingId : listing.id });

    ...

    $(this).on('listingUpdated', function(e, data) {
      // do something with data.listingId
    });
    ```

  **[[⬆]](#TOC)**


## <a name='modules'>模块</a>

  - 模块应该以 `!` 开始，这保证了如果一个有问题的模块忘记包含最后的分号在合并后不会出现错误
  - 这个文件应该以驼峰命名，并在同名文件夹下，同时导出的时候名字一致
  - 加入一个名为noConflict()的方法来设置导出的模块为之前的版本并返回它
  - 总是在模块顶部声明 `'use strict';`

    ```json
    // fancyInput/fancyInput.js

    !function(global) {
      'use strict';

      var previousFancyInput = global.FancyInput;

      function FancyInput(options) {
        this.options = options || {};
      }

      FancyInput.noConflict = function noConflict() {
        global.FancyInput = previousFancyInput;
        return FancyInput;
      };

      global.FancyInput = FancyInput;
    }(this);
    ```

    **[[⬆]](#TOC)**


## <a name='jquery'>jQuery</a>

  - 缓存jQuery查询

    ```json
    // bad
    function setSidebar() {
      $('.sidebar').hide();

      // ...stuff...

      $('.sidebar').css({
        'background-color': 'pink'
      });
    }

    // good
    function setSidebar() {
      var $sidebar = $('.sidebar');
      $sidebar.hide();

      // ...stuff...

      $sidebar.css({
        'background-color': 'pink'
      });
    }
    ```

  - 对DOM查询使用级联的 `$('.sidebar ul')` 或 `$('.sidebar ul')`，[jsPerf](http://jsperf.com/jquery-find-vs-context-sel/16)
  - 对有作用域的jQuery对象查询使用 `find`

    ```json
    // bad
    $('.sidebar', 'ul').hide();

    // bad
    $('.sidebar').find('ul').hide();

    // good
    $('.sidebar ul').hide();

    // good
    $('.sidebar > ul').hide();

    // good (slower)
    $sidebar.find('ul');

    // good (faster)
    $($sidebar[0]).find('ul');
    ```

    **[[⬆]](#TOC)**


## <a name='guide-guide'>JavaScript风格指南</a>

  - [Reference](https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide)

