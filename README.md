# Cheatsheet

## Css

### Position

- ``position:static``

	- The default positioning for all elements is position:static
	- the element is not positioned and occurs where it normally would in the document.

- ``position:relative``

	- you can use top or bottom, and left or right to move the element relative to where it would normally occur in the document.
	- still occupies that original space in the document, even though we have moved it.
	- If we set relative positioning on div-1, any elements within div-1 will be positioned relative to div-1.

- ``position:absolute``

	- When you specify position:absolute, the element is removed from the document and placed exactly where you tell it to go.


#### reference

http://www.barelyfitz.com/screencast/html-training/css/positioning/

### PIXI

#### Z-index problem
install [this](https://github.com/pixijs/pixi-display) first
直接把bin放到src
不知道為什麼npm package無法work

- Usage
	- z-order 越小越前面
	- z-index 越大越前面
	
> stage是一座城市,container是建築物,sprite是人,layer是公司,group是員工
> 如果layer是google office,那group就是googler

```js
// specify display list component
// 讓不同group中是有z-index差別的
app.stage = new PIXI.display.Stage();
app.stage.group.enableSort = true;

// 創兩個group(綠藍),有不同的z-index
// z-index = 0, sorting = true;
var greenGroup = new PIXI.display.Group(0, true);
greenGroup.on('sort', function (sprite) {
    //green bunnies go down
    sprite.zOrder = -sprite.y;
});

// z-index = 1, sorting = true, we can provide zOrder function directly in constructor
var blueGroup = new PIXI.display.Group(1, function (sprite) {
    //blue bunnies go up
    sprite.zOrder = +sprite.y;
});

// 在加入別的container時,像這樣寫,注意:ㄧ定要包一層layer,原因不明
app.stage.addChild(new PIXI.display.Layer(greenGroup));

// 在創建sprite時只要給他們指定好parentGroup就行了,不管他在哪個container,z的順序都會按照group排序
var bunny = new PIXI.Sprite(texture_blue);
bunny.parentGroup = blueGroup;
```

### Shell

- kill port

```
 kill -9 $(lsof -i:3000 -t)
```

### GIF

```
ffmpeg -i in.mov -s 600x400 -pix_fmt rgb24 -r 10 -f gif - | gifsicle --optimize=3 --delay=3 > out.gif
```

### GITHUB SSH

```
ssh-add ~/.ssh/id_rsa 
```