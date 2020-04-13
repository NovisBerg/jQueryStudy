# 一、DOM对象与jQuery对象的区别
1. DOM对象只能调用DOM方法、属性与事件；
2. jQuery对象只能调用jQuery方法、属性与事件；
3. 两者可以相互转换；
4. $只是jQuery的别名形式；
5. 每一个jQuery对象都是一个DOM对象的集合。

# 二、常用选择器
jQuery重点放在HTML页面里获取元素并对其进行操作，与CSS类似。有了jQuery，就能利用现有知识去发挥选择器的为例，在很大程度上简化JavaScript代码。

CSS中可以使用的选择器基本都可以用到jQuery中，反之则不然。
1. 选择器和包装集

通过使用选择器——基于元素的属性或元素在HTML文档中的位置，简明地表现元素。

如，选择器：p a

引用所有嵌套与\<p\>元素之内的超链接（\<a\>元素）组。jQuery利用同样的选择器，不仅支持目前CSS中使用的常见选择器，还支持尚未被大多数浏览器完全实现的更强大的选择器。收集一组元素，可以使用如下简单的语法：

`$(selector)或jQuery(selector)`

$()函数返回特别的JavaScript对象，它包含着与选择器相匹配的DOM元素的数组。该对象拥有大量预定义的有用方法，能够作用于该组元素。

用编程的化来说，这种构造成为包装器（wrapper），因为它用扩展功能来对匹配的元素进行包装。我们使用术语jQuery包装器或者包装集（wrapped set），来指能够在其上使用jQuery定义的方法去操作的、匹配元素的合集。

假定我们想选择带有CSS类notLongForThisWorld的所有\<div\>元素，jQuery语句如下：
`$('notLongForThisWorld')`
2. 基本选择器

基本选择器是jQuery中最常用的选择器，也是最简单的选择器。它通过元素id、class和标签名等来查找DOM元素。在网页中，每个id名称只能使用一次，class允许重复使用。

| 选择器 | 描述 | 返回 | 示例 |
| :----: | :----: | :----: | :----: |
| #id | 根据给定的id匹配一个元素 | 单个元素 | $("#test")选取id为test的元素 |
| .class | 根据给定的类名匹配元素 | 集合元素 | $(".test")选取所有class为test的元素 |
| element | 根据给定的元素名称匹配元素 | 集合元素 | $('p')选取所有的\<p\>元素 |
| select1,<br>select2,<br>select3... | 将每一个选择器匹配到的元素合并后一起返回 | 集合元素 | $("div,span,p.cls")选取所有\<div>，\<span>和拥有class为cls的\<p>标签的一组元素 |
| * | 匹配所有元素 | 集合元素 | $("*")选取所有的元素 |
可以使用这些基本选择器来完成绝大多数的工作。
# 三、 AJAX详解
AJAX全称为“Asynchronous JavaScript And XML”（异步JavaScript和XML），是指一种创建交互式网页应用的开发技术。其使用基于Web2.0标准的XHTML+CSS表示方式，使用DOM（Document Object Model）进行动态显示及交互，使用XML和XSLT进行数据交互即其相关操作，使用XMLHttpRequest进行异步数据查询、检索，使用JavaScript将所有的东西绑定在一起。

AJAX应用可以仅向服务器发送并取回必须的数据，它使用SOAP或其他一些基于XML的Wev Service接口，并在客户端采用JavaScript处理来自服务器的响应。因为在服务器和浏览器之间交换的数据大量减少，结果我们就能看到响应速度更快的应用。同时很多的处理工作可以在发出请求的客户端机器上完成，Web服务的处理时间也就减少了。

jQuery为AJAX带来方便，语法格式为：
`jQuery.ajax(url, [settings])`
通过HTTP请求加载远程数据。

最简单的情况下，$.ajax()可以不带任何参数直接使用。

需要注意的是：所有的选项都可以通过$.ajaxSetup()函数来全局设置。
- 回调函数
如果要处理$.ajax()得到的数据，则需要使用回调函数。beforeSend、error、dataFilter、success、complete.
    - beforeSend: 在发送请求之前调用，并且传入一个XMLHttpRequest作为参数；
    - error: 在请求出错时调用。传入XMLHttpRequest对象，描述错误类型的字符串以及一个异常对象（如果有的话）。
    - dataFilter: 在请求成功之后调用。传入返回的数据以及“dataType”参数的值。并且必须返回新的数据（可能是处理过的）传递给success回调函数；
    - success: 当请求之后调用。传入返回后的数据，以及包含成功代码的字符串；
    - complete: 当请求完成之后调用这个函数，无论成功或失败。传入XMLHttpRequest对象以及一个包含成功或错误代码的字符串。
    
- 数据类型

$.ajax()函数依赖服务器提供的信息来处理返回的数据。如果服务器报告说返回的数据是XML，那么返回的结果就可以用普通的XML方法或者jQuery的选择器来遍历。如果见得到其他类型，比如HTML，则数据就以文本形式来对待。

通过dataType选项还可以指定其他不同数据处理方式。除了单纯的XML，还可以指定 html、json、jsonp、script或者text。

其中，text和xml类型返回的数据不会经过处理。数据仅仅简单的将XMLHttpRequest的responseText或responseHTML属性传递给success回调函数，

'''注意'''，我们必须确保网页服务器报告的MIME类型与我们选择的dataType所匹配。比如说，XML的话，服务器端就必须声明 text/xml 或者 application/xml 来获得一致的结果。

如果指定为html类型，任何内嵌的JavaScript都会在HTML作为一个字符串返回之前执行。类似的，指定script类型的话，也会先执行服务器端生成JavaScript，然后再把脚本作为一个文本数据返回。

如果指定为json类型，则会把获取到的数据作为一个JavaScript对象来解析，并且把构建好的对象作为结果返回。为了实现这个目的，他首先尝试使用JSON.parse()。如果浏览器不支持，则使用一个函数来构建。JSON数据是一种能很方便通过JavaScript解析的结构化数据。如果获取的数据文件存放在远程服务器上（域名不同，也就是跨域获取数据），则需要使用jsonp类型。使用这种类型的话，会创建一个查询字符串参数 callback=? ，这个参数会加在请求的URL后面。服务器端应当在JSON数据前加上回调函数名，以便完成一个有效的JSONP请求。如果要指定回调函数的参数名来取代默认的callback，可以通过设置$.ajax()的jsonp参数。

注意，JSONP是JSON格式的扩展。他要求一些服务器端的代码来检测并处理查询字符串参数。

如果指定了script或者jsonp类型，那么当从服务器接收到数据时，实际上是用了&lt;script&gt;标签而不是XMLHttpRequest对象。这种情况下，$.ajax()不再返回一个XMLHttpRequest对象，并且也不会传递事件处理函数，比如beforeSend。
- 发送数据到服务器

默认情况下，Ajax请求使用GET方法。如果要使用POST方法，可以设定type参数值。这个选项也会影响data选项中的内容如何发送到服务器。

data选项既可以包含一个查询字符串，比如 key1=value1&amp;key2=value2 ，也可以是一个映射，比如 {key1: 'value1', key2: 'value2'} 。如果使用了后者的形式，则数据再发送器会被转换成查询字符串。这个处理过程也可以通过设置processData选项为false来回避。如果我们希望发送一个XML对象给服务器时，这种处理可能并不合适。并且在这种情况下，我们也应当改变contentType选项的值，用其他合适的MIME类型来取代默认的 application/x-www-form-urlencoded。
- 高级选项

global选项用于阻止响应注册的回调函数，比如.ajaxSend，或者ajaxError，以及类似的方法。这在有些时候很有用，比如发送的请求非常频繁且简短的时候，就可以在ajaxSend里禁用这个。更多关于这些方法的详细信息，请参阅下面的内容。

如果服务器需要HTTP认证，可以使用用户名和密码可以通过username和password选项来设置。

Ajax请求是限时的，所以错误警告被捕获并处理后，可以用来提升用户体验。请求超时这个参数通常就保留其默认值，要不就通过jQuery.ajaxSetup来全局设定，很少为特定的请求重新设置timeout选项。

默认情况下，请求总会被发出去，但浏览器有可能从他的缓存中调取数据。要禁止使用缓存的结果，可以设置cache参数为false。如果希望判断数据自从上次请求后没有更改过就报告出错的话，可以设置ifModified为true。

scriptCharset允许给&lt;script&gt;标签的请求设定一个特定的字符集，用于script或者jsonp类似的数据。当脚本和页面字符集不同时，这特别好用。

Ajax的第一个字母是asynchronous的开头字母，这意味着所有的操作都是并行的，完成的顺序没有前后关系。$.ajax()的async参数总是设置成true，这标志着在请求开始后，其他代码依然能够执行。强烈不建议把这个选项设置成false，这意味着所有的请求都不再是异步的了，这也会导致浏览器被锁死。

$.ajax函数返回他创建的XMLHttpRequest对象。通常jQuery只在内部处理并创建这个对象，但用户也可以通过xhr选项来传递一个自己创建的xhr对象。返回的对象通常已经被丢弃了，但依然提供一个底层接口来观察和操控请求。比如说，调用对象上的.abort()可以在请求完成前挂起请求。
