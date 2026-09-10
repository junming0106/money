````markdown
# 第二關：秦半兩方孔錢

## Step 1: 先看圖案座標，再輸入 qin 開始
先看座標圖：每一格都在 `z = 3` 這一面。  
橫著看是 `x`：　　　 `-2　-1　0　1　2`  
`y = 4`　　　　　　　`．　■　■　■　．`  
`y = 3`　　　　　　　`■　■　■　■　■`  
`y = 2`　　　　　　　`■　■　．　■　■`  
`y = 1`　　　　　　　`■　■　■　■　■`  
`y = 0`　　　　　　　`．　■　■　■　．`  

先找找看「．」在哪些座標，它們就是要變成空氣的位置。  
例如左上角是 `x=-2、y=4、z=3`，所以座標是 `pos(-2, 4, 3)`。  
在聊天欄輸入 `qin`，大括號裡的動作就會開始。  
現在裡面還沒有放方塊，所以遊戲畫面不會改變。

```blocks
player.onChat("qin", function () {

})
```

## Step 2: 做出橙色陶瓦平面
先做一整片橙色陶瓦，當作方孔錢的底。  
`ORANGE_TERRACOTTA` 就是橙色陶瓦。  
從 `pos(-2, 0, 3)` 放到 `pos(2, 4, 3)`。  
所以 `x` 從 `-2` 到 `2`，`y` 從 `0` 到 `4`，全部都在 `z=3`。  
`FillOperation.Replace` 會把這個範圍換成橙色陶瓦。  
輸入 `qin` 後，你會看到一個 5×5 的橙色平面。

```blocks
player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

})
```

## Step 3: 算出第一排左邊的空格
回到座標圖找 `y=4` 這一排。  
最左邊的「．」在 `x=-2`，所以是 `pos(-2, 4, 3)`。  
加入 `blocks.place`，把這個位置換成 `AIR`。  
`AIR` 就是空氣，原本的橙色陶瓦會消失。  
執行後，你會看到左上角少一格。

```blocks
player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

    // 第一排：.###.

    blocks.place(AIR, pos(-2, 4, 3))

})
```

## Step 4: 算出第一排右邊的空格
再看 `y=4` 這一排，右邊也有一個「．」。  
它在 `x=2`，所以座標是 `pos(2, 4, 3)`。  
再放一個 `AIR`，把這格橙色陶瓦拿掉。  
現在第一排左右兩邊都是空的。  
中間會留下三格橙色陶瓦。

```blocks
player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

    // 第一排：.###.

    blocks.place(AIR, pos(-2, 4, 3))

    blocks.place(AIR, pos(2, 4, 3))

    // 第二排不刪除：#####

})
```

## Step 5: 算出正中間的方孔
看看座標圖的正中央。  
中央的「．」在 `x=0、y=2`，而 `z` 一樣是 `3`。  
所以它的座標是 `pos(0, 2, 3)`。  
把這一格換成 `AIR`，橙色陶瓦就會消失。  
你會看到方孔錢中間出現一個小方孔。  
`y=3` 和 `y=1` 兩排沒有「．」，所以不用拿掉方塊。

```blocks
player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

    // 第一排：.###.

    blocks.place(AIR, pos(-2, 4, 3))

    blocks.place(AIR, pos(2, 4, 3))

    // 第二排不刪除：#####

    // 第三排：##.##

    blocks.place(AIR, pos(0, 2, 3))

    // 第四排不刪除：#####

})
```

## Step 6: 找出第五排左邊的空格
現在看座標圖的 `y=0` 這一排。  
左邊的「．」在 `x=-2`。  
把 `x=-2、y=0、z=3` 放進座標，就得到 `pos(-2, 0, 3)`。  
在這個位置放入 `AIR`。  
執行後，你會看到左下角的橙色陶瓦消失。

```blocks
player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

    // 第一排：.###.

    blocks.place(AIR, pos(-2, 4, 3))

    blocks.place(AIR, pos(2, 4, 3))

    // 第二排不刪除：#####

    // 第三排：##.##

    blocks.place(AIR, pos(0, 2, 3))

    // 第四排不刪除：#####

    // 第五排：.###.

    blocks.place(AIR, pos(-2, 0, 3))

})
```

## Step 7: 算出最後一格，完成方孔錢
第五排還有右邊一個「．」。  
它在 `x=2、y=0、z=3`，所以是 `pos(2, 0, 3)`。  
把這個位置換成 `AIR`。  
看看遊戲畫面，上下兩排都留下中間三格。  
中間也有一個方孔。  
秦半兩方孔錢就完成了。

```blocks
// 第二關：秦半兩方孔錢

player.onChat("qin", function () {

    // 建立5×5橙色陶瓦平面

    blocks.fill(

    ORANGE_TERRACOTTA,

    pos(-2, 0, 3),

    pos(2, 4, 3),

    FillOperation.Replace

    )

    // 第一排：.###.

    blocks.place(AIR, pos(-2, 4, 3))

    blocks.place(AIR, pos(2, 4, 3))

    // 第二排不刪除：#####

    // 第三排：##.##

    blocks.place(AIR, pos(0, 2, 3))

    // 第四排不刪除：#####

    // 第五排：.###.

    blocks.place(AIR, pos(-2, 0, 3))

    blocks.place(AIR, pos(2, 0, 3))

})
```
````



> Open this page at [https://junming0106.github.io/money/](https://junming0106.github.io/money/)

## Use as Extension

This repository can be added as an **extension** in MakeCode.

* open [https://minecraft.makecode.com/](https://minecraft.makecode.com/)
* click on **New Project**
* click on **Extensions** under the gearwheel menu
* search for **https://github.com/junming0106/money** and import

## Edit this project

To edit this repository in MakeCode.

* open [https://minecraft.makecode.com/](https://minecraft.makecode.com/)
* click on **Import** then click on **Import URL**
* paste **https://github.com/junming0106/money** and click import

#### Metadata (used for search, rendering)

* for PXT/minecraft
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
