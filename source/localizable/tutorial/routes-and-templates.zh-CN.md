In Super Rentals we want to arrive at a home page which shows a list of rentals. From there, we should be able to navigate to an about page and a contact page.

Ember provides a [robust routing mechanism](../../routing/) to define logical, addressable pages within our application.

## “关于我们” route

Let's start by building our "about" page. To create a new, URL addressable page in the application, we need to generate a route using Ember CLI.

如果执行 `ember help generate`，我们可以看到很多生成器工具，Ember用它们来自动生成各种资源文件。 我们将要用路由生成器来生成 `about`路由器。

```shell
ember generate route about
```

或者用命令简写

```shell
ember g route about
```

The output of the command displays what actions were taken by the generator:

```shell
installing route
  create app/routes/about.js
  create app/templates/about.hbs
updating router
  add route about
installing route-test
  create tests/unit/routes/about-test.js
```

A route is composed of the following parts:

  1. An entry in `/app/router.js`, mapping the route name to a specific URI. *`(app/router.js)`*
  2. A route handler JavaScript file, instructing what behavior should be executed when the route is loaded. *`(app/routes/about.js)`*
  3. A route template, describing the page represented by the route. *`(app/templates/about.hbs)`*

Opening `/app/router.js` shows that there is a new line of code for the *about* route, calling `this.route('about')` in the `map` function. Calling the function `this.route(routeName)`, tells the Ember router to load the specified route handler when the user navigates to the URI with the same name. In this case when the user navigates to `/about`, the route handler represented by `/app/routes/about.js` will be used. See the guide for [defining routes](../../routing/defining-your-routes/) for more details.

```app/router.js import Ember from 'ember'; import config from './config/environment';

const Router = Ember.Router.extend({ location: config.locationType, rootURL: config.rootURL });

Router.map(function() {this.route('about');});

export default Router;

    <br />”about“路由处理器会默认加载”about.hbs“模板页面。
    这以为这我们不需要在路由处理器”app/routes/about.js“文件中做任何修改来制定对应的模板文件”about.hbs“。
    
    生成器生成好所有路由相关配置，我们就可以直接开始逻辑代码和页面模板的开发了。
    在”关于我们“页面中，我们会加一些HTML代码用来描述网站的相关信息：
    ```app/templates/about.hbs
    <div class="jumbo">
      <div class="right tomster"></div>
      <h2>About Super Rentals</h2>
      <p>
        ”超级房屋出租“网站是一个有趣的项目，用来学习Ember框架。
        通过创建这个房屋出租网站，我们可以想象自己在旅行同时创建一个Eber应用。
      </p>
    </div>
    

Run `ember server` (or `ember serve` or even `ember s` for short) from the shell to start the Ember development server, and then go to [`http://localhost:4200/about`](http://localhost:4200/about) to see our new app in action!

## “联系我们” Route

我们接下来再创建另外一个路由器用来访问公司联系信息页面。我们还会通过生成器来添加一个路由器，一个 路由处理器和一个模板页面。

```shell
ember g route contact
```

The output from this command shows a new `contact` route in `app/router.js`, and a corresponding route handler in `app/routes/contact.js`.

In the route template `/app/templates/contact.hbs`, we can add the details for contacting our Super Rentals HQ:

```app/templates/contact.hbs 

<div class="jumbo">
  <div class="right tomster">
  </div>
  
  <h2>
    联系我们
  </h2>
  
  <p>
    超级出租公司的业务代表很高兴帮助您选择一个目的地或者回答您的任何问题。
  </p>
  
  <p>
    超级租赁总部 
    
    <address>
      1212 Test Address Avenue<br /> Testington, OR 97233
    </address>
    
    <a href="tel:503.555.1212">+1 (503) 555-1212</a><br /> <a href="mailto:superrentalsrep@emberjs.com">superrentalsrep@emberjs.com</a>
  </p>
</div>

    <br />现在我们已经完成了第二个路由器。
    如果访问 URL [`http://localhost:4200/contact`](http://localhost:4200/contact)，我们可以看到联系我们页面。
    
    ## Navigating with Links and the {{link-to}} Helper
    
    We'd like to avoid our users having knowledge of our URLs in order to move around our site,
    so let's add some navigational links at the bottom of each page.
    我们会在关于我们页面加上联系我们链接以及在联系我们页面加上关于我们链接。
    
    Ember has built-in template **helpers** that provide functionality for interacting with the framework.
    The [`{{link-to}}`](../../templates/links/) helper provides special ease of use features in linking to Ember routes.
    Here we will use the `{{link-to}}` helper in our code to perform a basic link between routes:
    
    ```app/templates/about.hbs{+9,+10,+11}
    <div class="jumbo">
      <div class="right tomster"></div>
      <h2>About Super Rentals</h2>
      <p>
        The Super Rentals website is a delightful project created to explore Ember.
        By building a property rental site, we can simultaneously imagine traveling
        AND building Ember applications.
      </p>
      {{#link-to 'contact' class="button"}}
        Get Started!
      {{/link-to}}
    </div>
    

`{{link-to}}` 辅助方法引入了name参数，用来标识需要跳转的目标路由地址，在这里是 `contact`。 这时我们访问关于我们页面 [`http://localhost:4200/about`](http://localhost:4200/about)，就可以看到一个可以跳转到联系我们的链接了。

![“超级访问出租”页面截图](../../images/routes-and-templates/ember-super-rentals-about.png)

接下来，我们要在联系我们页面在加入一个关于我们的跳转链接，这样我们就可以在`about` 和 `contact`两个页面来回跳转。.

```app/templates/contact.hbs 

<div class="jumbo">
  <div class="right tomster">
  </div>
  
  <h2>
    联系我们
  </h2>
  
  <p>
    超级出租公司的业务代表很高兴帮助您选择一个目的地或者回答您的任何问题。
  </p>
  
  <p>
    超级租赁总部 
    
    <address>
      1212 Test Address Avenue<br /> Testington, OR 97233
    </address>
    
    <a href="tel:503.555.1212">+1 (503) 555-1212</a><br /> <a href="mailto:superrentalsrep@emberjs.com">superrentalsrep@emberjs.com</a>
  </p> {{#link-to 'about' class="button"}} About {{/link-to}}
</div>

    <br />## 出租房屋列表路由
    我们的网站需要一个出租房屋列表供网站用户浏览。
    为了这样的一个列表我们需要创建第三个路由”rentals“。
    

Let's update the newly generated `app/templates/rentals.hbs` with some basic markup to add some initial content our rentals list page. We'll come back to this page later to add in the actual rental properties.

```app/templates/contact.hbs 

<div class="jumbo">
  <div class="right tomster">
  </div>
  
  <h2>
    欢迎！
  </h2>
  
  <p>
    我们希望你找到了梦寐以求的归宿。
  </p> {{#link-to 'about' class="button"}} About Us {{/link-to}}
</div>

    <br />## 首页 Route
    
    既然网站已经有了2个静态页面，我们可以制作一个首页来迎接网站用户了。
    目前我们应用的主页就是刚创建的房屋出租列表页。
    所以我们希望首页的route只是简单转发到我们刚创建的`rentals` route 。
    
    依照之前我们创建联系我们和关于我们页面的流程，我们要先创建一个叫 `index`的路由器。
    
    ```shell
    ember g route index
    

我们可以看到熟悉的route生成输出日志：

```shell
installing route
  create app/routes/index.js
  create app/templates/index.hbs
installing route-test
  create tests/unit/routes/index-test.js
```

跟我们之前创建的路由器不同， `index` 首页路由器比较特殊：它不需要在路由配置文件中做任何映射 。 我们将会在[nested routes](../subroutes) Ember的级联路由一章中会学到更多关于为什么首页index不需要路由映射。

我们现在可以为index首页开发单元测试了。 我们要测试的结果是首页能跳转到房屋出租列表 `rentals`，所以测试需要验证路由器的 [`replaceWith`](http://emberjs.com/api/classes/Ember.Route.html#method_replaceWith)方法可以被正确调用。 路由器中的`replaceWith`方法跟 `transitionTo`方法类似都是页面跳转，区别是`replaceWith`会把替换浏览器中的浏览历史，而 `transitionTo`则是将跳转地址到浏览历史中。 我们希望`rentals`路由成为主页，所以是用 `replaceWith`方法。 我们的测试需要先在路由中实现 `replaceWith`方法，同时断言`rentals`路由在调用时被正确传入。

```tests/unit/routes/index-test.js import { moduleFor, test } from 'ember-qunit';

moduleFor('route:index', 'Unit | Route | index');

test('should transition to rentals route', function(assert) { let route = this.subject({ replaceWith(routeName) { assert.equal(routeName, 'rentals', 'replace with route name rentals'); } }); route.beforeModel(); });

    <br />在index路由中，我们只需要添加“replaceWith”方法调用。
    
    ```app/routes/index.js
    import Ember from 'ember';
    
    export default Ember.Route.extend({
      beforeModel() {
        this.replaceWith('rentals');
      }
    });
    

现在当你访问根目录 `/`的时候会跳转到 `/rentals` URL。

## 在导航中加入旗帜区块

除了为每个路由提供按钮连接以为，我们还希望提供一个通用的标题旗帜区作为主页的链接。

首先，创建一个应用模板。输入命令：`ember g template application`.

```shell
installing template
  create app/templates/application.hbs
```

当首页模板 `application.hbs`存在后，你向其添加的内容会出现在网站的每个页面。现在我们加以下旗帜区域标记：

    app/templates/application.hbs
    <div class="container">
      <div class="menu">
        {{#link-to 'index'}}
          <h1 class="left">
            <em>SuperRentals</em>
          </h1>
        {{/link-to}}
        <div class="left links">
          {{#link-to 'about'}}
            About
          {{/link-to}}
          {{#link-to 'contact'}}
            Contact
          {{/link-to}}
        </div>
      </div>
      <div class="body">
        {{outlet}}
      </div>
    </div>

请注意在body div标签中的包含的`{{outlet}}` 代码块。 The [`{{outlet}}`](http://emberjs.com/api/classes/Ember.Templates.helpers.html#method_outlet) in this case is a placeholder for the content rendered by the current route, such as *about*, or *contact*.

Now that we've added routes and linkages between them, the three acceptance tests we created for navigating to our routes should now pass.

![通过了导航跳转测试](../../images/routes-and-templates/passing-navigation-tests.png)