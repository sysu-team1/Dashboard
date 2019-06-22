<!-- TOC -->

- [代码规范和设计说明](#代码规范和设计说明)
    - [python语言设计规范](#python语言设计规范)
    - [微信小程序界面设计规范](#微信小程序界面设计规范)

<!-- /TOC -->
# 代码规范和设计说明

## python语言设计规范
[Google的Python语言设计规范](https://zh-google-styleguide.readthedocs.io/en/latest/google-python-styleguide/contents/)


## 微信小程序界面设计规范
<div class="entry-content l-h-2x">
<center style="font-size: 12px;border-left: 4px solid #ff6225;background-color: #f1f1f1;border-bottom-right-radius: 2px;color: #3a3f51;margin: 1.6em -31px;">
</center> 
<div name="前言" data-unique="前言">
<hr>
<div name="目录规范" data-unique="目录规范"></div><h2>目录规范</h2> 
<div name="1.目录概述" data-unique="1.目录概述"></div><h3>1. 目录概述</h3> 
<div name="组件文件" data-unique="组件文件"></div><h4>组件文件</h4> 
<p>所有组件相关文件统一放在components目录下。</p> 
<div name="图片文件" data-unique="图片文件"></div><h4>图片文件</h4> 
<p>项目图片文件放置于根目录的images文件夹下，组件独有的图片放在当前组件images目录下</p> 
<div name="模型文件" data-unique="模型文件"></div><h4>模型文件</h4> 
<p>模型文件主要用于编写各类业务模型。项目模型文件放置于根目录的models文件夹下，组件相关模型放置于components目录下的models文件夹中。</p> 
<div name="行为文件" data-unique="行为文件"></div><h4>行为文件</h4> 
<p>行为文件放在所引用的组件目录下。</p> 
<hr>
<div name="WXML规范" data-unique="WXML规范"></div><h2>WXML规范</h2> 
<div name="1.WXML规范" data-unique="1.WXML规范"></div><h3>1. WXML规范</h3> 
<p>wxml标签可以单独出现的情况，尽量单独出现，如<code>&lt;input /&gt;</code>。</p> 
<pre><code class="hljs apache"><span class="hljs-section"><span class="hljs-section">&lt;input /&gt;</span></span></code></pre> 
<p>控制每行HTML的代码数量在50个字符以内，方便阅读浏览，多余的代码进行换行处理，标签所带属性每个属性间进行换行。</p> 
<pre><code class="hljs xml"><span class="hljs-tag"><span class="hljs-tag">&lt;</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">v-music</span></span></span><span class="hljs-tag">
</span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">wx:if</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"{{classic.type===200}}"</span></span></span><span class="hljs-tag">
</span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">img</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"{{classic.img}}"</span></span></span><span class="hljs-tag">
</span><span class="hljs-attr"><span class="hljs-tag"><span class="hljs-attr">content</span></span></span><span class="hljs-tag">=</span><span class="hljs-string"><span class="hljs-tag"><span class="hljs-string">"{{classic.content}}"</span></span></span><span class="hljs-tag">
&gt;</span></span>
<span class="hljs-tag"><span class="hljs-tag">&lt;/</span><span class="hljs-name"><span class="hljs-tag"><span class="hljs-name">v-music</span></span></span><span class="hljs-tag">&gt;</span></span></code></pre> 
<p>合理展现分离内容，不要使用内联样式。</p> 
<pre><code class="hljs javascript"><span class="hljs-comment"><span class="hljs-comment">//推荐使用</span></span>
&lt;image <span class="hljs-class"><span class="hljs-keyword"><span class="hljs-class"><span class="hljs-keyword">class</span></span></span></span>=<span class="hljs-string"><span class="hljs-string">"tag"</span></span>&gt;<span class="xml"><span class="hljs-tag"><span class="xml"><span class="hljs-tag">&lt;/</span></span><span class="hljs-name"><span class="xml"><span class="hljs-tag"><span class="hljs-name">image</span></span></span></span><span class="xml"><span class="hljs-tag">&gt;</span></span></span></span></code></pre> 
<div name="2.注释规范" data-unique="2.注释规范"></div><h3>2.注释规范</h3> 
<p>除组件外的其他块级元素，均需注释出其功能，并在其上下空出一行与其他代码进行区分。</p> 
<pre><code class="hljs q xml"><span class="hljs-tag">&lt;</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span>...<span class="hljs-tag">&lt;/</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span>
<span class="hljs-comment">//导航栏</span>
<span class="hljs-tag">&lt;</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span>...<span class="hljs-tag">&lt;/</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span>
<span class="hljs-tag">&lt;</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span>...<span class="hljs-tag">&lt;/</span><span class="hljs-built_in"><span class="hljs-tag"><span class="hljs-name">view</span></span></span><span class="hljs-tag">&gt;</span></code></pre> 
<div name="CSS规范" data-unique="CSS规范"></div><h3>CSS规范</h3> 
<div name="1.CSS规范" data-unique="1.CSS规范"></div><h4>1.CSS规范</h4> 
<p>在开发过程中rpx和px均可能用到，如通常情况下间距使用rpx，字体大小和边框等使用px，开发者根据实际情况而定。</p> 
<pre><code class="hljs scss"><span class="hljs-attribute">width</span>: <span class="hljs-number">100</span>rpx;
<span class="hljs-attribute">font-size</span>: <span class="hljs-number">14px</span>;</code></pre> 
<p>CSS代码需有明显的代码缩进。每一个样式类之间空出一行。</p> 
<pre><code class="hljs css"><span class="hljs-selector-class"><span class="hljs-selector-class">.v-tag</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">width</span></span>: <span class="hljs-number"><span class="hljs-number">100%</span></span>;
}
<span class="hljs-selector-class"><span class="hljs-selector-class">.v-container</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">width</span></span>: <span class="hljs-number"><span class="hljs-number">100%</span></span>;
}</code></pre> 
<p>尽量使用简写属性，并且同一属性放置在一起，避免散乱。</p> 
<pre><code class="hljs css"><span class="hljs-comment"><span class="hljs-comment">/**使用简写属性**/</span></span>
<span class="hljs-selector-class"><span class="hljs-selector-class">.v-image</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">margin</span></span>: <span class="hljs-number"><span class="hljs-number">0</span></span> auto;
}
<span class="hljs-comment"><span class="hljs-comment">/**同一属性放在一块**/</span></span>
<span class="hljs-selector-class"><span class="hljs-selector-class">.v-tag</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">margin-left</span></span>: <span class="hljs-number"><span class="hljs-number">10</span></span>rpx;
<span class="hljs-attribute"><span class="hljs-attribute">margin-right</span></span>: <span class="hljs-number"><span class="hljs-number">10</span></span>rpx
}</code></pre> 
<p>采用flex进行布局，禁止使用float以及vertical-align。</p> 
<pre><code class="hljs css"><span class="hljs-selector-class"><span class="hljs-selector-class">.container</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">disaplay</span></span>: flex;
<span class="hljs-attribute"><span class="hljs-attribute">flex-dirextion</span></span>: row
}</code></pre> 
<div name="2.注释规范12" data-unique="2.注释规范12"></div><h4>2.注释规范</h4> 
<p>成组的wxss规则之间用块状注释。请勿在代码后面直接注释。</p> 
<pre><code class="hljs css"><span class="hljs-comment"><span class="hljs-comment">/** 修改button默认的点击态样式类**/</span></span>
<span class="hljs-selector-class"><span class="hljs-selector-class">.button-hover</span></span> {
<span class="hljs-attribute"><span class="hljs-attribute">background-color</span></span>: red;
}</code></pre> 
<hr>
<div name="JS规范" data-unique="JS规范"></div><h2>JS规范</h2> 
<div name="1.JS规范" data-unique="1.JS规范"></div><h3>1.JS规范</h3> 
<div name="命名规范" data-unique="命名规范"></div><h4>命名规范</h4> 
<p>变量名以及函数名统一采用驼峰命名法，正常情况下函数名前缀需加上清晰的动词表示函数功能，私有函数或者属性以下划线开头表明。常量需用const 声明。类的命名首字母需大写。采用ES6 关键字let定义变量，尽量不使用var。</p> 
<pre><code class="hljs javascript"><span class="hljs-comment"><span class="hljs-comment">//定义常量</span></span>
<span class="hljs-keyword"><span class="hljs-keyword">const</span></span> a = <span class="hljs-number"><span class="hljs-number">1</span></span>
<span class="hljs-comment"><span class="hljs-comment">//定义变量</span></span>
<span class="hljs-keyword"><span class="hljs-keyword">let</span></span> imageContent =res.data
<span class="hljs-comment"><span class="hljs-comment">//函数命名</span></span>
getInfo:<span class="hljs-function"><span class="hljs-keyword"><span class="hljs-function"><span class="hljs-keyword">function</span></span></span><span class="hljs-function">(</span><span class="hljs-params"></span><span class="hljs-function"><span class="hljs-params"></span>)</span></span>{
<span class="hljs-keyword"><span class="hljs-keyword">return</span></span> <span class="hljs-string"><span class="hljs-string">''</span></span>;
}
<span class="hljs-comment"><span class="hljs-comment">//私有函数</span></span>
_getInfo:<span class="hljs-function"><span class="hljs-keyword"><span class="hljs-function"><span class="hljs-keyword">function</span></span></span><span class="hljs-function">(</span><span class="hljs-params"></span><span class="hljs-function"><span class="hljs-params"></span>)</span></span>{
<span class="hljs-keyword"><span class="hljs-keyword">return</span></span> <span class="hljs-string"><span class="hljs-string">''</span></span>;
}</code></pre> 
<div name="回调函数规范" data-unique="回调函数规范"></div><h4>回调函数规范</h4> 
<p>回调函数统一使用Promise函数的方式进行编写，回调成功的参数统一为res，错误参数为err。</p> 
<pre><code class="hljs javascript"><span class="hljs-comment"><span class="hljs-comment">// promise 处理回调</span></span>
<span class="hljs-keyword"><span class="hljs-keyword">let</span></span> back = <span class="hljs-keyword"><span class="hljs-keyword">new</span></span> <span class="hljs-built_in"><span class="hljs-built_in">Promise</span></span>(<span class="hljs-function"><span class="hljs-function">(</span><span class="hljs-params"><span class="hljs-function"><span class="hljs-params">resolve, reject</span></span></span><span class="hljs-function">) =&gt;</span></span> {
<span class="hljs-keyword"><span class="hljs-keyword">if</span></span> (<span class="hljs-comment"><span class="hljs-comment">/* 异步操作成功 */</span></span>){
resolve(value);
} <span class="hljs-keyword"><span class="hljs-keyword">else</span></span> {
reject(error);
}
});
back.then(<span class="hljs-function"><span class="hljs-function">(</span><span class="hljs-params"><span class="hljs-function"><span class="hljs-params">res</span></span></span><span class="hljs-function">) =&gt;</span></span> {
<span class="hljs-built_in"><span class="hljs-built_in">console</span></span>.log(<span class="hljs-string"><span class="hljs-string">'成功回调！'</span></span>, res);
}).catch(<span class="hljs-function"><span class="hljs-function">(</span><span class="hljs-params"><span class="hljs-function"><span class="hljs-params">err</span></span></span><span class="hljs-function">) =&gt;</span></span> {
<span class="hljs-built_in"><span class="hljs-built_in">console</span></span>.log(<span class="hljs-string"><span class="hljs-string">'失败回调！'</span></span>, error);
});</code></pre> 
<p>私有函数以及回调函数统一放置在生命周期函数后。<br> 删除js文件中未用到的生命周期函数，保持代码的整洁。</p> 
<pre><code class="hljs css"><span class="hljs-selector-tag"><span class="hljs-selector-tag">Pages</span></span>({
<span class="hljs-attribute"><span class="hljs-attribute">data</span></span>:{

},

<span class="hljs-selector-tag"><span class="hljs-selector-tag">onLoad</span></span><span class="hljs-selector-pseudo"><span class="hljs-selector-pseudo">:function(event)</span></span>{

},

_<span class="hljs-selector-tag"><span class="hljs-selector-tag">self</span></span><span class="hljs-selector-pseudo"><span class="hljs-selector-pseudo">:function()</span></span>{

}
})</code></pre> 
<p>每个函数之间用一个空行分离结构。</p> 
<div name="数据绑定变量定义规范" data-unique="数据绑定变量定义规范"></div><h4>数据绑定变量定义规范</h4> 
<p>所有涉及到数据绑定的变量均需在data中初始化。禁止在不定义的情况下直接setData。</p> 
<pre><code class="hljs javascript">Pages({
<span class="hljs-attr"><span class="hljs-attr">data</span></span>:{
 <span class="hljs-attr"><span class="hljs-attr">id</span></span> : <span class="hljs-literal"><span class="hljs-literal">null</span></span>
},

<span class="hljs-attr"><span class="hljs-attr">onLoad</span></span>:<span class="hljs-function"><span class="hljs-keyword"><span class="hljs-function"><span class="hljs-keyword">function</span></span></span><span class="hljs-function">(</span><span class="hljs-params"><span class="hljs-function"><span class="hljs-params">event</span></span></span><span class="hljs-function">)</span></span>{
<span class="hljs-keyword"><span class="hljs-keyword">let</span></span> id = event.target.dataset.id
<span class="hljs-keyword"><span class="hljs-keyword">this</span></span>.data.id = id
}
})</code></pre> 
<div name="点击事件规范" data-unique="点击事件规范"></div><h4>点击事件规范</h4> 
<p>点击事件函数命名方式为 on + 事件名 或者业务名。</p> 
<pre><code class="hljs javascript">onLike: <span class="hljs-function"><span class="hljs-keyword"><span class="hljs-function"><span class="hljs-keyword">function</span></span></span><span class="hljs-function">(</span><span class="hljs-params"><span class="hljs-function"><span class="hljs-params">event</span></span></span><span class="hljs-function">)</span></span>{
<span class="hljs-comment"><span class="hljs-comment">//....</span></span>
}</code></pre> 
<hr>
<div name="组件规范" data-unique="组件规范"></div><h2>组件规范</h2> 
<div name="组件名命名规范" data-unique="组件名命名规范"></div><h4>组件名命名规范</h4> 
<p>组件在使用时命名以 “v-”为开头的组件名，若组件名称为多个单词名拼接而成，采用 ' - ' 连接。组件标签在page页面使用时推荐使用单闭合标签（此条约束对于包含有slot的组件无效）v 来源于法语，单词 ‘vent’</p> 
<pre><code class="hljs apache"><span class="hljs-section"><span class="hljs-section">&lt;v-movies /&gt;</span></span></code></pre> 
<div name="触发事件规范" data-unique="触发事件规范"></div><h4>触发事件规范</h4> 
<p>组件点击触发事件建议用冒号分隔开</p> 
<pre><code class="hljs perl">&lt;v-component-tag-name <span class="hljs-keyword"><span class="hljs-keyword">bind</span></span>:myevent=<span class="hljs-string"><span class="hljs-string">"onMyEvent"</span></span> /&gt;</code></pre> 
<div name="externalClasses命名规范" data-unique="externalClasses命名规范"></div><h4>externalClasses命名规范</h4> 
<p>命名格式采用如下形式：</p> 
<pre><code class="hljs javascript">v-<span class="hljs-class"><span class="hljs-keyword"><span class="hljs-class"><span class="hljs-keyword">class</span></span></span><span class="hljs-class">-</span></span>{name}</code></pre> 
<p>name可自行定义</p> 
<pre><code class="hljs ruby">v-<span class="hljs-class"><span class="hljs-keyword"><span class="hljs-class"><span class="hljs-keyword">class</span></span></span><span class="hljs-class">-</span><span class="hljs-title"><span class="hljs-class"><span class="hljs-title">icon</span></span></span></span></code></pre> 
<hr>
<div name="组件样式规范" data-unique="组件样式规范"></div><h2>组件样式规范</h2> 
<p>**林间有风团队所产出的所有组件样式均应采用类的写法，且命名必须以 v- 开头，不允许使用内联样式以及id样式</p> 
<pre><code class="hljs css"><span class="hljs-selector-class"><span class="hljs-selector-class">.v-container</span></span>{
<span class="hljs-attribute"><span class="hljs-attribute">disaplay</span></span>: flex;
<span class="hljs-attribute"><span class="hljs-attribute">flex-dirextion</span></span>: row
}</code></pre> 
<hr>
<div name="标点规范" data-unique="标点规范"></div><h2>标点规范</h2> 
<p>1. JS语句无需以分号结束，统一省略分号<br>2. JS中一致使用反引号 ``或单引号' ' , 不使用双引号。<br>3. WXML、CSS、JSON中均应使用双引号。<br>4. CSS属性中冒号中后面用一个空格分隔开。<br>5. 执行一致的缩进（4个空格）<br>6. 执行一致的换行样式（'unix'）</p><hr class="content-copyright" style="margin-top:50px"><blockquote class="content-copyright" style="font-style:normal"></div>


<h2>其他规范</h2> 

<p>1. 变量与方法尽量使用驼峰式命名，并且注意避免使用 **$** 开头。 以 **$** 开头的标识符为**WePY**框架的内建属性和方法，可在**JavaScript**脚本中以 **this.** 的方式直接使用。具体请参考[API文档](https://tencent.github.io/wepy/document.html#/api?id=api)。
<br>2. 小程序入口、页面、组件文件名的后缀为.wpy；外链的文件可以是其它后缀
<br>使用ES6语法开发。 框架在ES6(ECMAScript 6)下开发，因此也需要使用ES6开发小程序，ES6中有大量的语法糖可以让我们的代码更加简洁高效。
<br>3. 使用Promise。 框架默认对小程序提供的API全都进行了 Promise 处理，甚至可以直接使用async/await等新特性进行开发。
<br>4. 事件绑定语法使用优化语法代替。
    
    * 原 ```bindtap="click"``` 替换为 ```@tap="click"```，原```catchtap="click"```替换为```@tap.stop="click"```。
    * 原 ```capture-bind:tap="click"``` 替换为 ```@tap.capture="click"```，原```capture-catch:tap="click"```替换为```@tap.capture.stop="click"。```
<br>5. 事件传参使用优化后语法代替。 原```bindtap="click" data-index={{index}}```替换为```@tap="click({{index}})"```。
<br>6. 自定义组件命名应避开微信原生组件名称以及功能标签<repeat>。 不可以使用input、button、view、repeat等微信小程序原生组件名称命名自定义组件；另外也不要使用WePY框架定义的辅助标签repeat命名。有关repeat的详细信息，请参见循环列表组件引用。
</p>