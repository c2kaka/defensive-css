# 最小内容尺寸
最小尺寸是属性，最小内容尺寸是一个尺寸值 。只不过有意思的是，当盒子的最小尺寸设置的值小于最小内容尺寸时，浏览器最终会把最小内容尺寸的计算值作为盒子的最小尺寸。
```css
.box {
    width: min-content;
    min-width: 200px; 
}
```

## Flexbox 和 Grid 中的最小内容尺寸
`min-width: auto`的不同计算方式:
- Flexbox: `min-width: auto`的计算值是`min-content`
- Grid: `min-width: auto`的计算值是`auto`
- Block: `min-width: auto`的计算值是`0`
- Inline: `min-width: auto`的计算值是`0`
- Inline-block: `min-width: auto`的计算值是`min-content`
- Table: `min-width: auto`的计算值是`0`

虽然在 CSS Flexbox 布局中，我们可以在 Flex 项目上显式设置 flex: 1 1 0% ，让 Flex 项目根据 Flex 容器的剩余空间或不足空间进行收缩与扩展，但是即使是这样，我们在使用 flex: 1 1 0% 对 Flex 项目进行收缩时，仍需特别注意，Flex 项目收缩之后的宽度不能小于 Flex 项目的最小内容尺寸（min-content） 。

为了避免 flex: 1 1 0% 引起的不必要麻烦，我们在编写 CSS 时应该注意，在使用 flex: 1 1 % 的 Flex 项目上**，**需要显式设置 min-width: 0 或 overflow: hidden (也可以是 auto 或 scroll )，只不过设置 overflow 时，需要根据具体需求来判断，如果不需要让 Flex 项目出现滚动条，建议 overflow 取 hidden 值 。

同样的，在 CSS Grid 布局中，Grid 项目收缩的时候，其宽度同样不能小于其最小内容尺寸。只不过，在 CSS Grid 布局中，我们常使用 1fr 来设置网格轨道，让相应的网格项目根据网格容器可用空间来进行收缩。也就是说，如果你在定义网格轨道时，碰到了 1fr 设置网格轨道尺寸时，需要使用下面三种方式来确保 Grid 网格项目不产生问题：

* 在定义网格轨道尺寸时，使用 minmax(0, 1fr) 来替代 1fr；
* 在设置为 1fr 网格轨道中的网格项目上显式设置 min-width 属性的值为 0；
* 在设置为 1fr 网格轨道中的网格项目上显式设置 overflow 属性的值为 hidden 或 auto 或 scroll 。如果不希望网格项目出现滚动条，则建议将 overflow 属性的值设置为 hidden。
* 虽然上面三种方式都可以避免 1fr 产生的问题，但我更建议使用 minmax(0, 1fr) 来替代 1fr。

最后简单地说，我们在编写 CSS 代码的时候，只要碰到了 flex:1 （或 flex: 1 1 0% 或 flex: 1 1 100% ）和在网格轨道设置 1fr 时，最好在对应的项目（Flex 项目或网格项目）上显式设置 min-width 的值为 0 ；而且使用 minmax(0, 1fr) 来替代 1fr 。这样你编写出的 CSS 更具防御性，代码也更健壮。
