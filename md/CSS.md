# 12 Flexbox布局
- 能让元素对不同的屏幕尺寸做好适应
- 盒指明空间的分布方式、内容的对齐方式和元素的视觉顺
- 盒依赖父子关系
- 在元素上声明display：flex或display：inline-flex该元素随之成为弹性容，控制子元素的布局
- 有直接子元素称为弹性元素
- **弹性盒的目的是实现一种特定的布局，即一维内容分布。也就是说，弹性盒最适合沿一个方向（或轴）布置内容。**
- 有时子元素的数量却不在我们的掌控之中，可能也不知道容器的宽度，使用弹性盒都能轻易解决


## 应用在弹性容器的属性
- **flex-direction**
如果你想要的布局是从上到下、从左至右、从右至左的，抑或是从下到上的，可以使用**flex-direction属性**控制排布弹性元素的主轴。
是从上到下、从左至右、从右至左的，抑或是从下到上
可以的值是row(默认) row-reverse column column-reverse
- **flex-wrap**
元素在弹性容器的主轴上放不下，默认情况下弹性元素不会换行，也不会自行调整尺寸，边界溢出
flex-wrap属性，允许弹性元素换行，变成多行或多列，或者缩减尺寸，挤在同一行。
取值nowrap wrap上 wrap-reverse

flex-flow属性是flex-direction和flex-wrap两个属性的简写形式

- **justify-content**
分配子元素的空余空间。
flex-start|flex-end|center|space-between|space-around|space-evenly

---

- 依赖父子关系
- 容器显示为块or行内？display: flex; displ: inline-flex
- 弹性元素布局方向flex-direction
- 元素太多，容器空间不够怎么办，减小元素尺寸还是是否允许换行flex-wrap
- 空白怎么处理？主轴：justify-content 垂轴：align-items  align-self
- 元素对齐
- 一维


flex-direction 4
flex-wrap 3
justify-content 6
align-items 5
align-self 6
align-content 7

## 弹性元素
flex-grow、flex-shrink和flex-basis属性用于控制弹性元素的弹性。这里所说的弹性是指弹性元素在主轴方向上可以增加或缩减多少尺寸。它们可以简写为flex
弹性容器根据弹性增长因子（flexgrowfactor）按比例分配额外的空间，或者根据弹性缩减因子（flexshrinkfactor）按比例缩小弹性元素，以防溢出

flex-grow属性定义有多余的空间时是否允许弹性元素增大，以及允许增大且有多余的空间时，相对其他同辈弹性元素以什么比例增大。只要大于或等于零即可。
如果flex属性没有设定增长因子和缩减因子，增长因子默认为1。然而，如果flex和flex-grow都没有声明，增长因子默认为0
如果在flex简写属性中没有声明，或者flex和flex-shrink都没有声明，缩减因子默认为1。如果是宽度不一样 缺少的空间/（（宽度1×缩减因子1）+...+（宽度N×缩减因子N））
flex-basis在分配空间前的初始尺寸，它可以是像素（px）或其他单位，默认为 auto（即项目的原始尺寸）。
min-width 是一个 CSS 属性，用于设置元素的 最小宽度，即元素的宽度不能小于该值。即使容器的宽度不足以容纳该元素，元素的宽度也不会小于 min-width 设置的值。
如果元素的实际内容宽度大于 min-width，那么这个元素的宽度将 根据内容的宽度自动扩展，而不会受 min-width 的限制。

flex简写属性。这个属性接受常规的全局属性值，包括initial、auto和none
initial 是一个 全局值，将属性恢复为默认值。flex: 0 1 auto;
auto 是 flex-basis 的默认值，表示项目的大小由内容的自然宽度或高度决定。flex: 1 1 auto;
none 是一个特殊的值，表示不允许元素在容器中伸展、收缩，元素的大小将由 flex-basis 决定，而不进行任何扩展或收缩。flex: 0 0 auto;

flex: <number> 这个值把弹性元素的增长因子设为<number>指定的数，同时把缩减因子设为0，把基准也设为0。

order属性用于修改单个弹性元素的显示顺序
order属性为负数的弹性元素显示在采用默认值o的弹性元素前面，
而order属性为正数的弹性元素显示在采用默认值0的弹性元素后面。



- flex-grow
- flex-shrink
- flex-basis
- min-width
- order
- flex


# 栅格布局
栅格布局是普适的布局系统。依赖行和列栅格之内可以嵌套栅格，层级不限，而且还可以在栅格中使用表格或弹性容器
栅格布局还有子栅格这个概念，它与嵌套的栅格容器不是一回事

栅格有两种：常规栅格和行内栅格。这两种栅格使用display属性的特殊值创建：grid和inline-grid。前者生成块级框，后者生成行内框

其中的元素根据栅格布局（而非块级布局）规则排布

表格自身就是一种栅格系统

栅格轨道gridtrack
栅格单元gridcell
栅格区域gridarea


grid-template-rows,grid-template-columns
取值none|<track-list>|<auto-track-list>

栅格线始终可以使用数字引1用，此外创作人员也可以为其命名又或者二者混用一条栅格线可以有多个名称
行和列不共用命名空间，因此可以像这样在两个上下文中重用名称。

---

来看看宽度固定的栅格轨道
grid-template-columns:[start col-a] 200px[col-b] 50%[col-c] 100px[stop end last];
[content] minmax（3em,100%)
