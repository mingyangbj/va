# va
多策略前端适配方案

解决的痛点：
   当前大部分的适配方案都是同比例缩放的，比如rem方案，这样在移动端上还可以，但是到了pc端，用一套设计稿的上下同比缩放可能有时候不满足需求。
比如需求为：
1，有一套1366的设计稿.要求：1366-1919之间，使用设计稿的px单位展示，不缩放不放大。在1920以上防止页面空白太多使用 同比放大展示。
现有的方案是无法满足这个需求是很麻烦的。

2，现有一个平台A按1366设计稿同比缩放实现的，而现在老板要求新页面按1920实现，旧的先不动，您该怎么处理呢？

3，还有其他很多问题。

总之同比缩放这个方案不灵活。

解决方法：
styles/view-auto-adapte.scss 中把设计稿宽度，css单位，业务代码写宽高的方法va等都做成了配置项。这样就灵活了。
用的时候直接拷贝styles/view-auto-adapte.scss，参考app.vue下面的
.view-auto{
    width: va(100);//页面组件的具体宽度，设计稿值
    height: va(100);//页面组件的具体高度，设计稿值
    background: #42b983;
}
这段代码使用即可。


具体分情况使用：
一，需求为同比例缩放1920设计稿：

--unit-base: 1vw;
--width-base: 1920;
--vw-num-base: 100;

/**
根据媒体查询的变量值，动态给公式赋值。达到返回不同策略的目的。
view auto
*/
@function va($px) {
@return calc(#{$px} * var(--vw-num-base) * var(--unit-base) / var(--width-base));
}

二，不同分辨率不同的策略。比如有一套1366的设计稿.要求：1366-1919之间，使用设计稿的px单位展示，不缩放不放大。在1920以上防止页面空白太多使用 同比放大展示。1366以下同比缩放
/**
unit-base:代表css单位：px，vw，rem等等。
width-base: 代表设计稿宽度。
vw-num-base：系统，用来切换px和vw时候使用。
*/
html {
@media screen and (max-width: 1365px) {
--unit-base: 1vw;
--width-base: 1920;
--vw-num-base: 100;
}

@media screen and (min-width: 1366px) and (max-width: 1920px) {
--unit-base: 1px;
--width-base: 1;
--vw-num-base: 1;
}

@media screen and (min-width: 1921px) {
--unit-base: 1vw;
--width-base: 1920;
--vw-num-base: 100;
}
}

/**
根据媒体查询的变量值，动态给公式赋值。达到返回不同策略的目的。
view auto
*/
@function va($px) {
@return calc(#{$px} * var(--vw-num-base) * var(--unit-base) / var(--width-base));
}

三，多设计稿可以对应多方法：比如现有一个平台A按1366设计稿同比缩放实现的，而现在老板要求新页面按1920实现，旧的先不动，您该怎么处理呢？
--unit-base: 1vw;
--width-base: 1366;
--vw-num-base: 100;

/**
根据媒体查询的变量值，动态给公式赋值。达到返回不同策略的目的。
view auto
*/
@function va($px) {
@return calc(#{$px} * var(--vw-num-base) * var(--unit-base) / var(--width-base));
}

/**
新增设计稿
*/
@function vb($px) {
@return calc(#{$px} * var(--vw-num-base) * var(--unit-base) / 1920);
}

四，其他一些小方法 您看着用

/**
传入设计稿宽度，单独适配页面使用。
view auto
*/
@function vaMq($px,$widthBase) {
@return calc(#{$px} * var(--vw-num-base) * var(--unit-base) / #{$widthBase});
}

/**
直接返回px  view px
*/
@function vp($px) {
@return calc(#{$px}px);
}

