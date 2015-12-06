[jsDelivr] [1] - 开源CDN
========

类似谷歌托管库，jsDelivr是一个开源[CDN] [6]，它允许开发人员举办自己的项目
和任何链接到我们的托管文件，在他们的网站上。

我们提供了一个稳定的CDN，可以在生产中使用，即使与大量流量的热门网站。
有没有带宽限制或高级功能和它的完全自由任何人使用。

所有类型的文件是允许的，包括JavaScript库，jQuery插件，CSS框架，字体等等。

您可以使用此回购协议，使自己的变化和提高jsDelivr的CDN的内容。
随意打开问题和拉请求，如果你觉得有什么应该改变。

该回购协议的所有更改都会同步到CDN。
这可能需要几分钟的变化出现在网站上。

[jsDelivr - 先进的开源公共CDN] [11]

[如何jsDelivr作品（过时）] [4]

[比较公共的CDN] [5]

[jsDelivr社区聊天] [12]

＃为什么jsDelivr？


性能和运行时间导向
--------------------

我们的公共CDN是建立在考虑性能和可靠性。一切都进行了优化，并不断完善，提供所有用户的最大速度和正常运行时间。性能始终处于监控，并且我们一直在寻找新的技术和服务提供者，可能会进一步提高我们的CDN。

停机时间，超时或慢的反应是完全不能接受的。这个想法是不是简单地提供一个公共的CDN，而是要提供最好的体验和坚如磐石的产品。



多CDN
---------

不同于竞争，jsDelivr使用多个CDN提供商，造成可能的最佳运行时间和性能。我们目前使用[MaxCDN] [7]，[CloudFlare的] [8]和[KeyCDN] [14]。

上的CDN提供商的顶部，jsDelivr还利用在位置定制的服务器，其中的CDN不必存在的点，以进一步优化的文件下载速度为邻近这些位置的用户。

如果一个CDN或自定义服务器出现故障，使用jsDelivr网站不会有任何问题，因为所有的流量将被立即重定向到剩余的运营商。


智能负载平衡
--------------------

jsDelivr使用[Cedexis] [10]与实际用户的性能数据（也称为RUM）作出路由决定。这些指标是从数百个网站收集和使用我们的负载均衡算法，使为服务内容的准确的决策。

所有的供应商（的CDN和自定义服务器）是由真正的用户来自世界各地的测试，每天数百万次。基于该信息，jsDelivr知道提供商是最快的为每个用户。每个用户得到基于他或她的位置，ISP和提供者的实时运行时间的唯一响应。

该系统也立即响应性能下降和供应商的停机时间。如果CDN是一个DDoS攻击下，其业绩下降在一些地方，在几秒钟的事算法将拿起变化，并开始服务于不同的供应商，所有受影响的用户。

SPDY
-----------------

我们所有的持久性有机污染物的支持[SPDY（https://developers.google.com/speed/spdy/）装载，使高性能的传输时可能。

＃【如何提交或更新项目（https://github.com/jsdelivr/jsdelivr/blob/master/CONTRIBUTING.md）
请参阅[CONTRIBUTING.md]（https://github.com/jsdelivr/jsdelivr/blob/master/CONTRIBUTING.md）有关如何将新的项目添加到jsDelivr说明。


自动更新
-------------

jsDelivr可以自动保持一个项目最多，最新的新版本发布。
配置过程简单快捷：您只需启用此功能的项目
是随着`info.ini`建立在其根目录中的`update.json`文件。

＃＃＃＃＃ 例([*/files/humane.js/update.json*](https://github.com/jsdelivr/jsdelivr/blob/master/files/humane.js/update.json)):

```json
{
"packageManager": "github",
"name": "humane.js",
"repo": "wavded/humane-js",
"files": {
"include": ["humane.min.js", "humane.js", "./themes/**/*"]
}
}
```

[完整文档可以在这里找到。] [13]


＃ 用法


URL结构
-------------

典型应用：
`//cdn.jsdelivr.net/{projectName} / {版本} / {文件}`
例如：`//cdn.jsdelivr.net / jQuery/1.11.0/ jquery.min.js`

如果你想在该版本文件夹作为一个压缩包中的所有文件：
`//cdn.jsdelivr.net/{projectName} / {version)} / {} PROJECTNAME .zip`

从他们的最新版本作为一个单一的分页文件下载的三个项目'`mainfile`：
`//cdn.jsdelivr.net/g/{projectName}，{项目名称}，{项目名称}`

您可以指定每个文件的特定版本或版本分支：
`//cdn.jsdelivr.net/g/{projectName} @ {版本}，{} PROJECTNAME @ {versionAlias}，{项目名称}`

您也可以从项目中（通常用于插件附带项目）选择多个文件：
`//cdn.jsdelivr.net/g/{projectName}@{version}({filepath1}+{filepath2}),{projectName}@{versionAlias},{projectName}`


版本走样
-------------

对于最新版本的使用：

`//cdn.jsdelivr.net/ {}项目名称/最新/ {文件}`

您也可以加载每个分支最新版本：

`//cdn.jsdelivr.net/ {} PROJECTNAME {/3.8/{file}`最新的3.8分支

`//cdn.jsdelivr.net/ {} PROJECTNAME / 3 / {file}`最新的3支

自动加载的项目使用的主要文件：

`//cdn.jsdelivr.net/{projectName} / latest/ mainfile`

根据项目的配置在'info.ini`与正确的MIME HTTP标头，jsDelivr将自动加载主文件。如果没有指定`mainfile`参数，请求将导致404错误。


装载有一个HTTP请求多个文件
--------------------------------------------

使用加载主文件的最新版本的多个项目：

`//cdn.jsdelivr.net /g/ abaaso,ace,alloyui`

主文件abaaso和用于其他项目的主文件的最新版本的负载3.8.15版：

`//cdn.jsdelivr.net /g/abaaso@3.8.15,ace,alloyui`

加载主文件的最新版本的所有文件和abaaso载荷版本分支3.8（例如版本16年8月3日：

`//cdn.jsdelivr.net / G / abaaso@3.8.15.ace.alloyui`


将多个文件，输入您要加载括号内（）由加+符号分隔的所有文件中的相对路径。支架可被编码为28％和29％无问题。

加载多个项目中的多个文件：

`//cdn.jsdelivr.net/g/jquery@2.1.0,angularjs@1.2.14(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

与往常一样，它支持版本的别名和最新版本：

`//cdn.jsdelivr.net/g/jquery,angularjs@1.2(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

`//cdn.jsdelivr.net/g/jquery,angularjs(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

文/ css`头：现在，如果组合中的所有文件都有一个'.css`扩展，则服务器将自动与`Content-Type的回应。在其他情况下，服务器响应'内容类型：应用程序/ javascript`头。

`//cdn.jsdelivr.net/g/angularui@0.4.0（角ui.min.css），animatecss @ 3.2.0`


第一3-4请求将比较慢，因为它们没有被缓存。随后，这些动态文件获取缓存并成为静态文件（同所有其他）。


API
---

jsDelivr有[一个全功能的API（https://github.com/jsdelivr/api），它也支持谷歌托管库和cdnjs


插件
---

### NPM jsdelivr

新公共管理的一个模块，它可以在您的Node.js应用程序中使用：

* https://github.com/jsdelivr/npm-jsdelivr

更多即将推出...


自定义CDN托管
---

如果您的项目不符合在GitHub上进行托管，或者您需要直接访问您的文件，这不是一个问题！
我们可以共同努力，建立一个自定义的配置为你的项目。这样，您就可以完全控制你的文件，而GitHub上的限制，并利用jsDelivr的全功率的能力。

这种定制主机可以是适合于：

*二进制托管。 Windows可执行文件和拉链。
*经常更新的文件。
*不能跟随jsDelivr文件结构的项目。
*其他一些用途，将打击所有我们的脑海中。

只要有一个请求，或了解更多信息，请发送电子邮件至[jimaek]（https://github.com/jimaek）。

jsDelivr为您提供帮助，而不是限制。即使你需要的不是上面列出的东西，请随时与我们联系。


贡献业绩数据
---

** jsDelivr **使用真实用户性能数据（也称为RUM）作出路由决策。这个数据是从数百个网站收集和用在我们的负载平衡算法，以使基于实时性能度量准确的决定。

这就是为什么我们提供的能力，所有用户来帮助我们。这个数据是非常重要的，我们鼓励所有的用户参与。

所有你需要做的是包括前`</boby>`在你的网站下面的JavaScript代码。
然后执行该代码在用户每次访问您的网站的时间。它使用自己的浏览器来测试延迟到我们的CDN提供商，并收集性能和可用性指标。

这些基准是完全透明的用户，并没有对浏览以任何方式影响。我们存储以下信息：

*性能指标，我们每一个供应商。
*可用性指标来我们每一个供应商。
*浏览器的用户代理
*前三用户的IP地址的八位字节

我们的JS代码以2秒的延时执行，并测试我们所有的供应商，除非中断。这个测试不会在您的网站的性能或用户浏览体验的影响。

```html
<script>
(function(a,b,c,d,e){function f(){var a=b.createElement("script");a.async=!0;
a.src="//radar.cedexis.com/1/11475/radar.js";b.body.appendChild(a)}/\bMSIE 6/i
.test(a.navigator.userAgent)||(a[c]?a[c](e,f,!1):a[d]&&a[d]("on"+e,f))})
(window,document,"addEventListener","attachEvent","load");
</script> 

或者你也可以将其包含在A / G /组合URL。只需在末尾添加'jsdelivr-rum`，包括我们的JavaScript。例如：

http://cdn.jsdelivr.net /g/ jQuery@2.1,jsdelivr,rum`


[隐私政策的数据贡献（http://www.cedexis.com/legal/privacy.html）


  [1]：http://www.jsdelivr.com
  [2]：https://github.com/jimaek/jsdelivr/blob/master/files/abaaso/info.ini
  [3]：http://refresh-sf.com/yui/
  [4]：http://blog.maxcdn.com/load-balancing-multiple-cdns-jsdelivr-works/
  [5]：http://www.cdnperf.com/
  [6]：http://en.wikipedia.org/wiki/Content_delivery_network
  [7]：http://tracking.maxcdn.com/c/47243/36539/378
  [8]：http://www.cloudflare.com/
  [9]：https://github.com/jsdelivr/jsdelivr/fork
  [10]：http://www.cedexis.com/
  [11]：https://hacks.mozilla.org/2014/03/jsdelivr-the-advanced-open-source-public-cdn/
  [12]：https://gitter.im/jsdelivr/jsdelivr
  [13]：https://github.com/jsdelivr/libgrabber#add-updatejson-schema
  [14]：https://www.keycdn.com/
[jsDelivr][1] - Open Source CDN
========

类似谷歌托管库，jsDelivr是一个开源 [CDN][6] 它允许开发者举办自己的项目，任何人都可以在自己的网站链接到我们托管的文件.

我们提供了一个稳定的CDN，可以在生产中使用，即使与大量流量的热门网站。 有没有带宽限制或高级功能和它的完全自由任何人使用。.

所有类型的文件是允许的，包括JavaScript库，jQuery插件，CSS框架，字体等等。 您可以使用此回购协议，使自己的变化和提高jsDelivr的CDN的内容。 随意打开问题和拉请求，如果你觉得有什么应该改变。 该回购协议的所有更改都会同步到CDN。 这可能需要几分钟的变化出现在网站上。.

[jsDelivr – The advanced open source public CDN][11]

[How jsDelivr works (outdated)][4]

[Compare public CDNs][5]

[jsDelivr community chat][12]

# Why jsDelivr?


Performance and Uptime Oriented
--------------------

Our public CDN is built with performance and reliability in mind. Everything is optimized and being constantly improved to offer all users maximum speed and uptime. Performance is monitored at all times, and we are always looking into new technologies and providers that may further improve our CDN.

Downtime, timeouts or slow responses are simply unacceptable. The idea is not to simply offer a public CDN, but to offer the best possible experience and a rock-solid product.



Multi-CDN
---------

Unlike the competition, jsDelivr uses multiple CDN providers, resulting in the best possible uptime and performance. We currently use [MaxCDN][7], [CloudFlare][8], and [KeyCDN][14].

On top of CDN providers, jsDelivr also utilizes custom servers in locations where CDNs don't have points of presence to further optimize the speed of file downloads for users near those locations.

If a CDN or custom server goes down, websites that use jsDelivr won't have any issues because all traffic will be instantly redirected to remaining operational providers.


Smart Load Balancing
--------------------

jsDelivr uses [Cedexis][10] with real user performance data (also known as RUM) to make its routing decisions. These metrics are gathered from hundreds of websites and are used in our load balancing algorithm to make accurate decisions for serving content.

All providers (CDNs and custom servers) are tested millions times per day by real users from all over the world. Based on this information, jsDelivr knows what provider is the fastest for each user. Each user gets a unique response based on his or her location, ISP, and the providers' uptime in real time.

This system also responds immediately to performance degradation and downtime of providers. If a CDN is under a DDoS attack, and their performance drops in some locations, in matter of seconds the algorithm will pick up the change and start serving a different provider to all affected users.

SPDY
-----------------

All of our POPs support [SPDY](https://developers.google.com/speed/spdy/) loading, allowing performant transfers when possible.

# [How to submit or update projects](https://github.com/jsdelivr/jsdelivr/blob/master/CONTRIBUTING.md)
Refer to [CONTRIBUTING.md](https://github.com/jsdelivr/jsdelivr/blob/master/CONTRIBUTING.md) for instructions on how to add a new project to jsDelivr.


Auto-Updating
-------------

jsDelivr can automatically keep a project up-to-date as new versions are released.
Configuration is fast and easy: All you need to enable this feature for a project
is to create an `update.json` file in its root directory along with the `info.ini`.

##### Example ([*/files/humane.js/update.json*](https://github.com/jsdelivr/jsdelivr/blob/master/files/humane.js/update.json)):

```json
{
  "packageManager": "github",
  "name": "humane.js",
  "repo": "wavded/humane-js",
  "files": {
    "include": ["humane.min.js", "humane.js", "./themes/**/*"]
  }
}
```

[Full documentation is available here.][13]


# Usage


URL Structure
-------------

Typical usage:  
`//cdn.jsdelivr.net/{projectName}/{version}/{file}`  
Example: `//cdn.jsdelivr.net/jquery/1.11.0/jquery.min.js`

When you want all the files in that version folder as a single compressed archive:  
`//cdn.jsdelivr.net/{projectName}/{version}/{projectName}.zip`

Downloads the three projects' `mainfile` from their latest versions as a single collated file:  
`//cdn.jsdelivr.net/g/{projectName},{projectName},{projectName}`

You may specify a specific version or version-branch per file:  
`//cdn.jsdelivr.net/g/{projectName}@{version},{projectName}@{versionAlias},{projectName}`

You may also select more than one file from a project (typically for plug-ins that ship with the project):  
`//cdn.jsdelivr.net/g/{projectName}@{version}({filepath1}+{filepath2}),{projectName}@{versionAlias},{projectName}`


Version aliasing
-------------

For latest version use:

`//cdn.jsdelivr.net/{projectName}/latest/{file}`

You can also load latest versions per branch:

`//cdn.jsdelivr.net/{projectName}/3.8/{file}` Latest in 3.8 branch

`//cdn.jsdelivr.net/{projectName}/3/{file}` Latest in 3 branch

To automatically load the main file of a project use:

`//cdn.jsdelivr.net/{projectName}/{version}/mainfile`

Depending on the project, jsDelivr will automatically load the main file as configured in `info.ini` with correct MIME HTTP headers. If no `mainfile` parameter was specified, the request will result in 404 error.


Load multiple files with single HTTP request
--------------------------------------------

Load multiple projects using the lastest version of the main file:

`//cdn.jsdelivr.net/g/abaaso,ace,alloyui`

Load version 3.8.15 of the main file for abaaso and the latest version of the main file for the other projects:

`//cdn.jsdelivr.net/g/abaaso@3.8.15,ace,alloyui`

Load the latest version of the main file for all files and for abaaso loads version branch 3.8 (e.g. version 3.8.16):

`//cdn.jsdelivr.net/g/abaaso@3.8,ace,alloyui`


To combine multiple files enter the relative paths to all files you want to load inside brackets () separated by a plus + symbol. Brackets can be encoded as %28 and %29 without issues.

Load multiple files from multiple projects:

`//cdn.jsdelivr.net/g/jquery@2.1.0,angularjs@1.2.14(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

As always it supports version aliasing and latest versions:

`//cdn.jsdelivr.net/g/jquery,angularjs@1.2(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

`//cdn.jsdelivr.net/g/jquery,angularjs(angular.min.js+angular-resource.min.js+angular-animate.min.js+angular-cookies.min.js+angular-route.min.js+angular-sanitize.min.js)`

Now if all files in the combination have a `.css` extension then the server will automatically respond with `Content-Type: text/css` header. In all other cases the server responds with `Content-Type: application/javascript` header.

`//cdn.jsdelivr.net/g/angularui@0.4.0(angular-ui.min.css),animatecss@3.2.0`


The first 3-4 requests will be slower, as they are not yet cached. Afterwards, these dynamic files get cached and become static files (same as all others).


API
---

jsDelivr has [a fully featured API](https://github.com/jsdelivr/api) that also supports Google Hosted Libraries and cdnjs


Plugins
---

### npm jsdelivr

An npm module that can be used in your node.js applications:

* https://github.com/jsdelivr/npm-jsdelivr

More coming soon...


Custom CDN Hosting
---

If your project does not qualify to be hosted in GitHub or you need direct access to your files, it's not a problem!
We can work together and setup a custom configuration for your project. This way, you can have full control over your files, without the restrictions of GitHub, and the ability to utilize the full power of jsDelivr.

This kind of custom hosting can be suitable for:

* Binary hosting. Windows executable files and zips.
* Frequently updated files.
* Projects that can't follow jsDelivr file structure.
* Some other use that will blow all of our minds.

Simply send an email to [jimaek](https://github.com/jimaek) with a request or for more information.

jsDelivr is here to help and not to limit. Even if what you need is not listed above, feel free to contact us.


Contribute Performance Data
---

**jsDelivr** uses real user performance data (also known as RUM) to make its routing decisions. This data is gathered from hundreds of websites and is used in our load balancing algorithm to make accurate decisions based on real time performance metrics.

This is why we offer the ability to all users to help us out. This data is very important and we encourage all users to participate.

All you have to do is include the following JavaScript code in your website before `</body>`.
This code is then executed each time a user visits your website. It uses their browser to test the latency to our CDN providers and gather performance and availability metrics.

These benchmarks are completely transparent to the user and do not impact on browsing in any way. We store the following information:

* Performance metrics to each of our providers.
* Availability metrics to each of our providers.
* Browser’s User-Agent
* First three octets of the user’s IP address

Our JS code is executed with a 2 second delay and tests all of our providers unless interrupted. This testing does not impact on your website performance or user browsing experience.

```html
<script>
(function(a,b,c,d,e){function f(){var a=b.createElement("script");a.async=!0;
a.src="//radar.cedexis.com/1/11475/radar.js";b.body.appendChild(a)}/\bMSIE 6/i
.test(a.navigator.userAgent)||(a[c]?a[c](e,f,!1):a[d]&&a[d]("on"+e,f))})
(window,document,"addEventListener","attachEvent","load");
</script> 
```

Alternatively you can also include it in a /g/ combined URL. Simply add `jsdelivr-rum` at the end to include our javascript. For example:

`http://cdn.jsdelivr.net/g/jquery@2.1,jsdelivr-rum`


[Privacy Policy for Data Contribution](http://www.cedexis.com/legal/privacy.html)


  [1]: http://www.jsdelivr.com
  [2]: https://github.com/jimaek/jsdelivr/blob/master/files/abaaso/info.ini
  [3]: http://refresh-sf.com/yui/
  [4]: http://blog.maxcdn.com/load-balancing-multiple-cdns-jsdelivr-works/
  [5]: http://www.cdnperf.com/
  [6]: http://en.wikipedia.org/wiki/Content_delivery_network
  [7]: http://tracking.maxcdn.com/c/47243/36539/378
  [8]: http://www.cloudflare.com/
  [9]: https://github.com/jsdelivr/jsdelivr/fork
  [10]: http://www.cedexis.com/
  [11]: https://hacks.mozilla.org/2014/03/jsdelivr-the-advanced-open-source-public-cdn/
  [12]: https://gitter.im/jsdelivr/jsdelivr
  [13]: https://github.com/jsdelivr/libgrabber#add-updatejson-schema
  [14]: https://www.keycdn.com/
