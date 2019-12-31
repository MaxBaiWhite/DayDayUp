# 《flex布局》

# 容器

1. flex-direction   
flex-direction决定主轴的方向
    1. row（默认值）：主轴为水平方向，起点在左端。
    2. row-reverse：主轴为水平方向，起点在右端。
    3. column：主轴为垂直方向，起点在上沿。
    4. column-reverse：主轴为垂直方向，起点在下沿
2. flex-wrap   
flex-wrap如果一条轴排不下，如何换行
    1. nowrap（默认）：不换行。
    2. row-reverse：换行，第一行在上方。
    3. wrap-reverse：换行，第一行在下方。
3. flex-flow   
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap
4. justify-content   
justify-content属性定义了项目在主轴上的对齐方式
    1. flex-start（默认值）：左对齐
    2. flex-end：右对齐
    3. center： 居中
    4. space-between：两端对齐，项目之间的间隔都相等。
    5. space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍
5. align-items  
align-items属性定义项目在交叉轴上如何对齐。
    1. flex-start：交叉轴的起点对齐。
    2. flex-end：交叉轴的终点对齐。
    3. center：交叉轴的中点对齐。
    4. baseline: 项目的第一行文字的基线对齐。
    5. stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
6. align-content  
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
    1. flex-start：与交叉轴的起点对齐。
    2. flex-end：与交叉轴的终点对齐。
    3. center：与交叉轴的中点对齐。
    4. space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
    5. space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    6. stretch（默认值）：轴线占满整个交叉轴。
    
## 子项目
1. order   
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0

2. flex-grow
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

3. flex-shrink
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

4. flex-basis   
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。

5. flex   
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。

6. align-self  
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。