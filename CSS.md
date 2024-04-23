在 CSS 中直接根据页面宽度设置元素的 margin-right 属性，你可以使用媒体查询（media query）结合 CSS 变量（CSS variables）来实现。

以下是一个示例，展示了如何在 CSS 中根据页面宽度设置元素的 margin-right 属性：
html

<template>
  <div class="my-element">
    <!-- 元素内容 -->
  </div>
</template>

<style>
.my-element {
  margin-right: var(--element-margin);
}

@media (min-width: 1920px) {
  :root {
    --element-margin: 15%;
  }
}

@media (max-width: 1919px) {
  :root {
    --element-margin: 8%;
  }
}
</style>


## 字体vm和em的区别
ChatGPT

在CSS中，em和rem是相对于父元素或根元素的字体大小单位，而rem是相对于根元素的字体大小单位。

    em单位：相对于父元素的字体大小。如果应用在父元素上，则其值等于父元素的字体大小。如果应用在子元素上，则其值等于子元素的字体大小乘以em的数值。

    rem单位：相对于根元素的字体大小。rem单位始终相对于根元素的字体大小。根元素是通常是<html>元素。

这些单位的主要区别在于它们相对的参考点不同：

    em是相对于父元素的字体大小，因此可以实现继承的效果。例如，如果父元素的字体大小为16像素，子元素的字体大小设置为1.5em，那么子元素的字体大小将会是24像素（1.5乘以16）。
    rem是相对于根元素的字体大小。由于根元素的字体大小通常是浏览器默认的字体大小（通常为16像素），所以rem单位提供了一种相对于浏览器默认字体大小的一致性参考。这使得在整个页面中使用rem单位更加方便，可以实现全局的字体大小控制。

总结起来，em单位是相对于父元素的字体大小，而rem单位是相对于根元素的字体大小，它们可以用于相对字体大小的设置，但参考点不同。选择使用哪种单位取决于你希望相对于父元素或根元素进行字体大小的调整。


## vw和%的区别
ChatGPT

在 CSS 中，vw（视窗宽度单位）和 %（百分比单位）都可以用于设置元素的宽度或大小，但它们有一些区别。

    vw 单位：相对于视窗宽度的百分比。1vw 等于视窗宽度的 1%。这意味着使用 vw 单位可以根据视窗的宽度进行自适应调整。例如，如果视窗宽度为 1000px，一个元素的宽度设置为 50vw，那么该元素的宽度将是视窗宽度的 50% 即 500px。

    % 单位：相对于父元素的百分比。使用 % 单位可以根据父元素的大小进行相对调整。例如，如果一个元素的宽度设置为 50%，那么该元素的宽度将是父元素宽度的 50%。

主要区别如下：

    vw 是相对于视窗宽度的百分比，而 % 是相对于父元素宽度的百分比。
    vw 单位不受父元素的宽度影响，而 % 单位会受到父元素宽度的影响。
    vw 单位可以用于实现响应式设计，根据视窗宽度的变化而自适应调整大小。
    % 单位更适合在相对布局中使用，根据父元素的大小进行调整。

选择使用哪种单位取决于你的设计需求和布局目标。如果你想根据视窗宽度进行自适应调整，那么使用 vw 单位是一个不错的选择。而如果你需要相对于父元素进行调整，则可以使用 % 单位。

# `_blank`的作用
在提供的代码中，'_blank' 是 window.open() 函数的第二个参数，用于指定打开链接的目标窗口或标签的名称。'_blank' 是一个特殊的目标名称，表示在新的、无名的浏览器窗口或标签中打开链接。


## 关于webGL的错误
1.
    Unchecked runtime.lastError: Could not establish connection. Receiving end does not exist.
2.
    three.r134.min.js:6 THREE.WebGLRenderer: Error creating WebGL context.
3.
    Uncaught Error: Error creating WebGL context.
    at new Qs (three.r134.min.js:6)
    at d.initThree (vanta.globe.min.js:1)
    at new h.VantaBase (vanta.globe.min.js:1)
    at new d (vanta.globe.min.js:1)
    at Object.h.<computed> [as GLOBE] (vanta.globe.min.js:1)
    at (index):205
4.
    VM12:1 [Deprecation] 'window.webkitStorageInfo' is deprecated. Please use 'navigator.webkitTemporaryStorage' or 'navigator.webkitPersistentStorage' instead.


# 关于display:flex
flex-wrap: wrap; 是 Flexbox 布局的一个属性，用于控制当子元素在容器中无法一行显示时的换行行为。

默认情况下，Flexbox 容器的子元素会尽量在一行内显示，即使它们超出了容器的宽度，会导致子元素压缩或溢出容器。但是，通过设置 flex-wrap: wrap;，可以强制子元素在需要时换行并形成多行布局。

# 关于position：relative、position: absolute 和 position: fixed
position: relative、position: absolute 和 position: fixed 是 CSS 中用于控制元素定位的属性值。

    position: relative：相对定位。元素相对于其正常位置进行定位，通过设置 top、right、bottom 和 left 属性来调整元素的位置。相对定位不会脱离文档流，其他元素仍然会占据原来的位置。

    position: absolute：绝对定位。元素脱离文档流，相对于其最近的非 static 定位的父元素（或者 <html> 元素）进行定位。通过设置 top、right、bottom 和 left 属性来确定元素的位置。绝对定位的元素不会影响其他元素的布局。

    position: fixed：固定定位。元素脱离文档流，相对于浏览器视口进行定位。无论页面滚动与否，固定定位的元素始终保持在固定的位置。通过设置 top、right、bottom 和 left 属性来确定元素的位置。

这些定位属性可以与其他 CSS 属性（如 top、right、bottom、left）一起使用，以精确控制元素在页面中的位置和布局。

请注意，对于绝对定位和固定定位，如果没有设置 top、right、bottom 和 left 中的任何一个属性，元素将会覆盖在其正常位置上，不会发生偏移。
