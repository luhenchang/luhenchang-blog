---
theme: qklhk-chocolate
highlight: agate
---
# 一、动态效果
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[Compose](https://developer.android.com/reference/kotlin/androidx/compose)目前官方并没有二级联动相关的支持。官方目前在[material3](https://developer.android.com/reference/kotlin/androidx/compose/material/package-summary)中提供了[ScrollableTabRow](https://developer.android.com/reference/kotlin/androidx/compose/material/package-summary)配合[HorizontalPager](https://developer.android.com/reference/kotlin/androidx/compose/material/package-summary)可以实现Tab和Pager联动。昨天在项目中有此需求，写完之后做个笔记。

![700_1694584434.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c649893a9bb24310bba68a163827bb3b~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=245&h=501&s=1567429&e=gif&f=108&b=fdfdfd)

# 二、遇到问题
   &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;快速写一个联动嵌套。利用ScrollableTabRow和HorizontalPager进行一级联动。在HorizontalPager切换的每个Pager内部也是ScrollableTabRow和HorizontalPager联动的二级页面。
## 1、代码编写
![多级联动01.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e11a1c3b91cb4e09af18b5a3c1c89227~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1384&h=260&s=1690151&e=gif&f=167&b=d389b3)

```kt
@Composable
fun ScrollableTabRowSimple() {
    val scope = rememberCoroutineScope()
    val titles = remember {
        mutableStateListOf("掘金小册", "字节内部课")
    }
    val pagerState = rememberPagerState(pageCount = { titles.size })
    Column {
        ScrollableTabRow(
            modifier = Modifier
                .fillMaxWidth()
                .wrapContentHeight(),
            selectedTabIndex = pagerState.currentPage,
            contentColor = Color.Black,
            divider = {},
            indicator = {
            }
        ) {
            titles.forEachIndexed { index, data ->
                val selected = pagerState.currentPage == index
                Box(
                    Modifier
                        .height(40.dp)
                        .fillMaxWidth()
                        .clickable {
                            scope.launch {
                                //Tab被点击后让Pager中内容动画形式滑动到目标页
                                pagerState.scrollToPage(index, 0f)
                            }
                        }, contentAlignment = Alignment.Center
                ) {
                    Text(
                        text = data,
                        fontSize = if (selected) 18.sp else 16.sp,
                        fontWeight = if (selected) FontWeight.Bold else FontWeight.Normal,
                        color = if (selected) MaterialTheme.colorScheme.primary else Color.Black
                    )
                }
            }
        }
        HorizontalPager(
            state = pagerState,
            modifier = Modifier
                .fillMaxHeight()
        ) { pagePosition ->
            SecondPager()
        }
    }
}

private fun SecondPager() {
    val data = remember {
        mutableStateListOf("Android", "IOS", "人工智能", "开发人员", "代码人生", "阅读", "购买")
    }
    val pagerState = rememberPagerState(pageCount = { data.size })
    val scope = rememberCoroutineScope()
    Column {
        ScrollableTabRow(
            modifier = Modifier
                .wrapContentWidth()
                .wrapContentHeight(),
            selectedTabIndex = pagerState.currentPage,
            contentColor = Color.Black,
            edgePadding = 10.dp,
            divider = {},
            minTabWidth = 76.dp,
            indicator = { tabPositions ->
                if (tabPositions.isNotEmpty()) {
                    PagerTabIndicator(
                        tabPositions = tabPositions,
                        pagerState = pagerState,
                        paddingIndicatorWidth = 35.dp
                    )
                }
            }
        ) {
            data.forEachIndexed { index, data ->
                val selected = pagerState.currentPage == index
                Box(
                    Modifier
                        .height(40.dp)
                        .wrapContentWidth()
                        .clickable {
                            scope.launch {
                                pagerState.scrollToPage(index, 0f)//Tab被点击后让Pager中内容动画形式滑动到目标页
                            }
                        }, contentAlignment = Alignment.Center

                ) {
                    Text(
                        text = data, fontSize = 13.sp,
                        fontWeight = if (selected) FontWeight.Bold else FontWeight.Normal,
                        color = if (selected) MaterialTheme.colorScheme.primary else Color.Black
                    )
                }
            }
        }
        HorizontalPager(
            state = pagerState,
            modifier = Modifier
                .fillMaxHeight()
        ) { pagePosition ->
            Box(
                Modifier
                    .fillMaxSize(),
                contentAlignment = Alignment.Center
            ) {
                Text(text = "页面：：=${pagePosition}")
            }
        }


    }
}
```
## 2、遇到问题
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在二级页面滑动到最后一个，进行继续滑动切换一级页面时候出现了如下冲突：

![多级联动02.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c4fe3ac6681147d9a35cf94a29a0fe17~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1384&h=260&s=1369948&e=gif&f=125&b=fefefe)

同样一级第二个页面“字节内部课”第一个Pager手势向右滑动到"掘金小册"也出现同样的问题。

![scroll004.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/11ccb0747bc84f8cbbe64e7151beab52~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1384&h=260&s=1477630&e=gif&f=133&b=ffffff)

看到上面效果，大家可能会想到了NestedScrollConnection，是否可以处理。在官方查阅[NestedScrollConnection文档](https://developer.android.com/jetpack/compose/touch-input/pointer-input/scroll#nested-scrolling-interop)时候看到并非支持所有的滑动组件，而**HorizontalPager**是否有相关的支持，接下来分析。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/587db2ff9f1c4566afec6aac2c061f1f~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=2134&h=748&s=1354273&e=png&b=fefefe)
# 三、分析问题
## 1、HorizontalPager源码
问题分析之前，先粗略浏览一下HorizontalPager源码，如果有时间可以自行仔细查看源码。此篇基于
androidx.compose.foundation:foundation:"1.5.0" 查看：

**1、HorizontalPager方法最终将数据打包给了内部的Pager**
```kt
@Composable
@ExperimentalFoundationApi
fun HorizontalPager(
    state: PagerState,
    modifier: Modifier = Modifier,
    contentPadding: PaddingValues = PaddingValues(0.dp),
    pageSize: PageSize = PageSize.Fill,
    beyondBoundsPageCount: Int = 0,
    pageSpacing: Dp = 0.dp,
    verticalAlignment: Alignment.Vertical = Alignment.CenterVertically,
    flingBehavior: SnapFlingBehavior = PagerDefaults.flingBehavior(state = state),
    userScrollEnabled: Boolean = true,
    reverseLayout: Boolean = false,
    key: ((index: Int) -> Any)? = null,
    pageNestedScrollConnection: NestedScrollConnection = PagerDefaults.pageNestedScrollConnection(
        Orientation.Horizontal
    ),
    pageContent: @Composable PagerScope.(page: Int) -> Unit
) {
    Pager(
        state = state,
        modifier = modifier,
        contentPadding = contentPadding,
        pageSize = pageSize,
        beyondBoundsPageCount = beyondBoundsPageCount,
        pageSpacing = pageSpacing,
        orientation = Orientation.Horizontal,
        verticalAlignment = verticalAlignment,
        horizontalAlignment = Alignment.CenterHorizontally,
        flingBehavior = flingBehavior,
        userScrollEnabled = userScrollEnabled,
        reverseLayout = reverseLayout,
        key = key,
        pageNestedScrollConnection = pageNestedScrollConnection,
        pageContent = pageContent
    )
}
```
**2、Pager内部通过PageState对LazyLayout进行了各种滑动和效果等测量记录：**<br/>


```Kotlin
@Composable
internal fun Pager(
    /** Modifier to be applied for the inner layout */
    modifier: Modifier,
    /** State controlling the scroll position */
    state: PagerState,
    .........
) {
    require(beyondBoundsPageCount >= 0) {
        "beyondBoundsPageCount should be greater than or equal to 0, " +
            "you selected $beyondBoundsPageCount"
    }

    val overscrollEffect = ScrollableDefaults.overscrollEffect()

    val pagerItemProvider = rememberPagerItemProviderLambda(
        state = state,
        pageContent = pageContent,
        key = key
    ) { state.pageCount }

    val measurePolicy = rememberPagerMeasurePolicy(
        state = state,
        contentPadding = contentPadding,
        reverseLayout = reverseLayout,
        orientation = orientation,
        beyondBoundsPageCount = beyondBoundsPageCount,
        pageSpacing = pageSpacing,
        pageSize = pageSize,
        horizontalAlignment = horizontalAlignment,
        verticalAlignment = verticalAlignment,
        itemProviderLambda = pagerItemProvider,
        pageCount = { state.pageCount },
    )

    val pagerFlingBehavior = remember(flingBehavior, state) {
        PagerWrapperFlingBehavior(flingBehavior, state)
    }

    val pagerSemantics = if (userScrollEnabled) {
        Modifier.pagerSemantics(state, orientation == Orientation.Vertical)
    } else {
        Modifier
    }

    val semanticState = rememberPagerSemanticState(
        state,
        reverseLayout,
        orientation == Orientation.Vertical
    )

    LazyLayout(
        modifier = modifier
            .then(state.remeasurementModifier)
            .then(state.awaitLayoutModifier)
            .then(pagerSemantics)
            .lazyLayoutSemantics(
                itemProviderLambda = pagerItemProvider,
                state = semanticState,
                orientation = orientation,
                userScrollEnabled = userScrollEnabled,
                reverseScrolling = reverseLayout
            )
            .clipScrollableContainer(orientation)
            .pagerBeyondBoundsModifier(
                state,
                beyondBoundsPageCount,
                reverseLayout,
                orientation
            )
            .overscroll(overscrollEffect)
            .scrollable(
                orientation = orientation,
                reverseDirection = ScrollableDefaults.reverseDirection(
                    LocalLayoutDirection.current,
                    orientation,
                    reverseLayout
                ),
                interactionSource = state.internalInteractionSource,
                flingBehavior = pagerFlingBehavior,
                state = state,
                overscrollEffect = overscrollEffect,
                enabled = userScrollEnabled
            )
            .dragDirectionDetector(state)
            .nestedScroll(pageNestedScrollConnection),
        measurePolicy = measurePolicy,
        prefetchState = state.prefetchState,
        itemProvider = pagerItemProvider
     )

}

    
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  *val overscrollEffect = ScrollableDefaults.overscrollEffect()*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  overscrollEffect用于记录滚动效果，最终通过上的.scrollable(..overscrollEffect = overscrollEffect,...)进行绑定，并最终通过
DraggableElement持有的ScrollDraggableState通过dragBy->dispatchScroll->最终并提供过渡滚动绘制必要的数据
overscrollEffect.applyToScroll(scrollDelta, source, performScroll)。最终通过
**LazyLayout**的Modifier.overscroll(overscrollEffect)来渲染过渡滚动效果。有时间可以自己看看内部源码。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *val measurePolicy = rememberPagerMeasurePolicy(state = state...)*<br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; measurePolicy 通过滑动过程进行对其页面测量并通过PagerState.applyMeasureResult将测量结果返回给PagerState。用于更新PageState里面的canScrollForward、scrollToBeConsumed、canScroollforward、canScrollBackward等值。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *val pagerFlingBehavior = remember(flingBehavior, state) {PagerWrapperFlingBehavior(flingBehavior, state)}* 对快速等滑动提供给更好的多交互效果。自行查看源码。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; *val pagerSemantics = if (userScrollEnabled) {
    Modifier.pagerSemantics(state, orientation == Orientation.Vertical)
} else {
    Modifier
}* <br/>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pagerSemantics点进去可以发现，它决定着滑动切换到下一个页面或者上一个页面【上下左右】，这里可以看到userScrollEnabled决定是否可以进行页面切换。也可以看到最终调用了PagerState的animateToNextPage和animateToPreviousPage，并在其方法内部进行具体的页面跳转索引计算，最后进行跳转同时进行页面测量更新。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/eddc82f9f9b947c189e66a46fc4d30d2~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=2704&h=1214&s=2082724&e=png&b=1d1d20)


## 2、PagerState相关参数

PagerState在上面部分可以看到，滑动部分和测量部分的很多信息都被更新到其中，作为提供给开发者的状态集，很有必要看看其内部各种参数：

### 1、PagerState

  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `如果经常查看相关事件源码的就明白，基本能够提供滑动相关状态和数据的就是它了。`大概浏览，基本都可以看到当前的页面索引、总的页面数...

![image.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/57b27993e8234432a614830840243fed~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=2662&h=924&s=2214900&e=png&b=3f4042)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  currentPage： currentPage一直会提供当前手势过程中的页面，用来获取操作过程中所操作的页面索引，进行其他设置。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  pageCount：总的Pager个数

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; initialPage:初始化首次显示的页面，可以用来设置其他页面跳转到此页面时候设置跳转目标Pager


&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  currentPageOffsetFraction：

![animalenenen.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dade4182a7c44c5596eafa70ed718991~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=600&h=307&s=4914658&e=gif&f=331&b=242424)

如上所示：当前页面拖动距离距离自身未拖动时候的距离、此数值是-0.5-0.0-0.5之间，默认未拖动情况是0.0，当手势拖动向左滑动到和上一个页面中间此数值从0.0变小逐渐接近到-0.5会变为上一个页面的0.5。相反手势向右拖动，此数值从0.0逐渐接近0.5，当页面滑动到一半时候立马变为-0.4同样变为下一页距离默认位置之间的距离。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; initialPage:初始化首次显示的页面，可以用来设置其他页面跳转到此页面时候设置跳转目标Pager

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; interactionSource:
当此列表被拖动时用于分发拖动事件。如果你想知道事件（或动画滚动）是否正在进行中，请使用 isScrollInProgress 属性。当然了也可以用interactionSource。当拖动时候下面应该为true，松手之后变为false。

```js
val draggablePagerState = pagerState.interactionSource.collectIsDraggedAsState().value  
Log.e("pagerState===",draggablePagerState.toString())
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; settledPage：某次滑动结束从当前页面跳转到下一页面【前后页面】，如果最终滑动结束会返回拖动页面索引和结束时候页面所在的索引。例如页面0拖动向左滑动，结束之后，返回0和1表示从0滑动到了1。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; scrollToPage：滚动（立即跳转）到指定页面。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; animateScrollToPage： 以动画方式滚动到指定的 [page]

###  2、userScrollEnabled
（来设置是否可以用户滑动）


###  3、pageNestedScrollConnection
这个目前看像是NestedScrollConnection可以用来监听滑动嵌套布局在滑动时候的相关数据

###  4、flingBehavior
(快速慢速等滑动行为) 例如快速滑动松开手之后能够滑动的最大页数，以及慢速滑动或者快速滑动所执行动画等....自行了解。

###  5、PagerState参数
根据上面PagerState提供的参数，可以知道当前页面索引、总的页面个数、设置可否滑动、初始化页面索引、接收子节点滑动交互信息、拖动事件等、crollToPage和animateScrollToPage也就是我们可以控制一级页面滑动到上一页或下一页。

## 3、分析
我们可以看到非一级页面切换的零界点滑动切换二级页面，是没有任何问题的。

![horoscroll_gif01.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b4a070baa65d4bcc9da32abe4f551d0c~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1352&h=438&s=2047017&e=gif&f=56&b=393d49)

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;整体来看布局结构是滑动容器**HorizontalPager**嵌套了另一个HorizontalPager。每一个**HorizontalPager**
其内部实现了手势拖动下各个Pager之间的切换。首先我们知道，两个可滑动的容器嵌套，其事件消费优先级默认PointerEventPass.Main，所以会让子页面优先消费。而当二级**HorizontalPager**滑动到最后一个页面继续向左边拖动，此时事件不在消费，而是交给父级HorizontalPager去处理了滑动。

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;就在这种临界条件下出现了滑动问题：

####  1、临界页面

![hozirotal_animal_03.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/848816dcb79642f6aece1af2add44c31~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1352&h=438&s=713019&e=gif&f=20&b=393d49)

![horizatal_animal02.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/80ff58fceb22419f937ba65965c1d5f8~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1352&h=438&s=1859631&e=gif&f=46&b=393d49)

####  2、事件冲突











如下图、当临界页面继续向左拖动











# 三、解决问题
# 三、实现