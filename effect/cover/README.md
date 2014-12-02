# Cover

Cover动画组件，提供cover显示隐藏、定位、自定义形状和背景等功能特性。



## 调用方式

```js
// 绑定cover到.cover
$(".cover").cover(option);

// 直接绑定到body上，与$("body").cover(option)等效
$.cover(option);
```


## 配置说明


配置信息可以通过js传参，也可以通过元素的`data-*`的方式。

配置信息也可以被trigger的`data-*`来重置。

具体配置信息如下：


<table>
    <tr>
        <th>name</th>
        <th>type</th>
        <th>default</th>
        <th>description</th>
    </tr>
    <tr>
        <td>trigger</td>
        <td>element</td>
        <td>null</td>
        <td>cover触发显示的元素。</td>
    </tr>
    <tr>
        <td>dismiss</td>
        <td>null</td>
        <td>null</td>
        <td>cover触发隐藏的元素。</td>
    </tr>
    <tr>
        <td>background</td>
        <td>string</td>
        <td>随机</td>
        <td>cover的背景色，可通过trigger的data-background配置重置。下同</td>
    </tr>
    <tr>
        <td>duration</td>
        <td>int</td>
        <td>1000</td>
        <td>动画耗时</td>
    </tr>
    <tr>
        <td>startPos</td>
        <td>string</td>
        <td>"source"</td>
        <td>
            <p>cover动画开始时的位置，默认为`source`（trigger的中心位置）。</p>
            <p>可选参数：source|top|center|bottom</p>
        </td>
    </tr>
    <tr>
        <td>offset</td>
        <td>Array</td>
        <td>[0,0]</td>
        <td>cover在startPos的基础上的偏移量。</td>
    </tr>
    <tr>
        <td>expandAxis</td>
        <td>string</td>
        <td>'x'</td>
        <td>cover扩展方向，可选 x|y|xy</td>
    </tr>
    <tr>
        <td>isFloat</td>
        <td>BOOL</td>
        <td>true</td>
        <td>触发元素是否保持在cover上方</td>
    </tr>
    <tr>
        <td>zIndex</td>
        <td>int</td>
        <td>999</td>
        <td>cover的z-index</td>
    </tr>
    <tr>
        <td>callback</td>
        <td>functon</td>
        <td>function(){}</td>
        <td>事件回调，有两个参数，第一个参数为事件类型，第二个参数为当前cover对象。</td>
    </tr>
</table>


## DEMO展示

````iframe
<!-- CSS -->
<style type="text/css">
body{position: absolute;top:0px;left:0px;width: 100%;height:100%;}
.ui-frozen-cover{overflow: hidden;position: absolute;top:0px;left:0px;width: 100%;height:100%;}
.item{width:100%;height:25%;display: -webkit-box;-webkit-box-pack:center; -webkit-box-align:center}
.close{position:fixed;top:10px;right:10px;display: block;width:50px;height:50px;color:#fff;border:#fff 1px solid; text-align: center;border-radius: 50px;line-height: 50px;display: none;z-index: 2000}
.title{color:#fff;display: block;text-align: center;font-size: 24px;-webkit-transition:all .5s .3s;}
.info{color:#fff;display: block;text-align: center;font-size: 12px;-webkit-transition:all .5s;top:50%;width:100%;top:50%;position: absolute;z-index: 2000;opacity: 0;-webkit-transform:translateY(50px);}
.info.show{opacity: 1;-webkit-transform:translateY(0);}
</style>

<!-- HTML -->
<div class="ui-frozen-cover" id="cover" data-start-pos="source" data-trigger=".item" data-dismiss=".close">
    <div class="close" >关闭</div>
    <div class="item" style="background:#35a;" data-background="#35a">
        <div class="title">网页重构</div>
    </div>
    <div class="item" style="background:#880;" data-background="#880">
        <div class="title">前端开发</div>
    </div>
    <div class="item" style="background:#4a3;" data-background="#4a3">
        <div class="title">交互设计</div>
    </div>
    <div class="item" style="background:#099;" data-background="#099">
        <div class="title">视觉设计</div>
    </div>
</div>
<div class="text">
    <div class="info">
        <p>全球最牛网页重构</p>
    </div>
    <div class="info">
        <p>全球最牛前端开发</p>
    </div>
    <div class="info">
        <p>全球最牛交互设计</p>
    </div>
    <div class="info">
        <p>全球最牛视觉设计</p>
    </div>

</div>


<!-- JS -->
<script type="text/javascript">
$(".ui-frozen-cover").cover({
    callback:function(type,obj){
        switch(type){
            case "show":
            covershow(obj);
            break;
            case "hide":
            coverhide(obj);
            break;
            case "hidden":
            coverhidden(obj);
            break;
            case "shown":
            covershown(obj);
            break;
        }
        
    }
});
function covershow(cover){
    if(!cover._isShown){
        var title=cover.currentTrigger.find('.title'),
            index=$(".item").index(cover.currentTrigger);

        title.css({
            '-webkit-transform':'translateY('+(cover.position.screenHeight/2-title.offset().top-30)+'px)'
        });
        $('.info').eq(index).css({
            "-webkit-transition-delay":".5s"
        })
        $('.info').eq(index).addClass('show');
    }
};
function coverhide(cover){
    var title=cover.currentTrigger.find('.title'),
        index=$(".item").index(cover.currentTrigger);

    title.css({
        '-webkit-transform':'translateY(0px)'
    })
    $('.info').eq(index).css({
            "-webkit-transition-delay":"0s"
        })
    $('.info').eq(index).removeClass('show');
};
function covershown(cover){
    $('.close').show();
};
function coverhidden(){
    $('.close').hide();
};
    
</script>
````
