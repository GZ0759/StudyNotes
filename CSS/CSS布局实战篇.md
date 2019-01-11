
<!-- TOC -->

- [居中](#居中)
  - [水平居中](#水平居中)
  - [垂直居中](#垂直居中)
- [多列布局](#多列布局)
  - [一列定宽，一列自适应](#一列定宽一列自适应)
  - [一列不定宽，一列自适应](#一列不定宽一列自适应)
  - [等分多列布局](#等分多列布局)
  - [等高多列布局](#等高多列布局)
- [flex布局](#flex布局)
- [圣杯布局](#圣杯布局)
- [双飞翼布局](#双飞翼布局)

<!-- /TOC -->

# 居中

## 水平居中

1. 使用`text-align + inline-block`

此方案兼容性较好，可兼容至IE8，对于IE567并不支持inline-block，需要使用css hack进行兼容

```html
<div class="demo1">
	<div class="parent" style="text-align: center>
		<div class="child" style="display: inline-block;">DEMO</div>
	</div>
</div>
```

2. 使用`table + margin`

此方案兼容至IE8，可以使用`<table/>`代替css写法，兼容性良好

```html
<div class="demo2">
	<div class="parent">
		<div class="child" style="display: table;margin: 0 auto;">DEMO</div>
	</div>
</div>
```

3. 使用`absolute + transform`

此方案兼容至IE9，因为transform兼容性限制。如果`.child`为定宽元素，可以使用`margin-left:-50px`，兼容性极佳。

```html
<div class="demo3">
	<div class="parent" style="position: relative;width: 100%;height:1.7em">
		<div class="child" style="position: absolute;left: 50%;transform: translateX(-50%);">
            DEMO
        </div>
	</div>
</div>
```

4. 使用`flex + justify-content`

flex是一个强大的css，生而为布局，它可以轻松的满足各种居中、对其、平分的布局要求，但由于现浏览器兼容性问题，此方案很少被使用。

```html
<div class="demo4">
	<div class="parent" style="display: flex;justify-content: center">
		<div class="child" style="margin: 0 auto;">DEMO</div>
	</div>
</div>
```

## 垂直居中

1. 使用`table-cell + vertial-align`

可替换成`<table />`布局，兼容性良好

```html
<div class="demo2">
	<div class="parent" style="display: table-cell; vertical-align: middle; height: 4em">
		<div class="child">DEMO</div>
	</div>
</div>
```

2. 使用`absolute + transform`

存在css3兼容问题，定宽兼容性良好

```html
<div class="demo2">
	<div class="parent" style="position: relative; height: 4em">
		<div class="child" style="position: absolute; top: 50%; transform: translateY(-50%);">DEMO</div>
	</div>
</div>
```


3. 使用`flex + align-items`

高版本浏览器兼容，低版本不适用

```html
<div class="demo2">
	<div class="parent" style="display: flex; align-items: center; height: 4em">
		<div class="child">DEMO</div>
	</div>
</div>
```

# 多列布局

## 一列定宽，一列自适应

1. 使用`float + margin`

此方案对于定宽布局比较好，不定宽布局推荐方法2

```html
<div class="demo4">
	<div class="parent">
		<div class="left" style="float: left; width: 100px">
			<p>left</p>
		</div>
		<div class="right" style="margin-left: 120px">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```

2. 使用`float + overflow`

此方案不管是多列定宽或是不定宽，都可以完美实现，同时可以实现等高布局

```html
<div class="parent">
	<div class="left" style="float: left; width: 100px; margin-right: 20px">
		<p>left</p>
	</div>
	<div class="right" style="overflow: hidden">
		<p>right</p>
		<p>right</p>
	</div>
</div>
```

3. 使用`table`

```html
<div class="demo4">
	<div class="parent" style="display: table; width: 100%; table-layout: fixed">
		<div class="left" style="display: table-cell; width: 100px; padding-right: 20px;">
			<p>left</p>
		</div>
		<div class="right" style="display: table-cell; border-left: solid;">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```

3. 使用`flex`

```html
<div class="demo4">
	<div class="parent" style="display: flex">
		<div class="left" style="width: 100px;padding-right: 20px;">
			<p>left</p>
		</div>
		<div class="right" style="flex: 1;border-left: solid">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```



## 一列不定宽，一列自适应

1. 使用`float + overflow`

```html
<div class="demo5">
	<div class="parent">
		<div class="left" style="float: left; margin-right: 20px">
			<p style="width: 200px;">left</p>
		</div>
		<div class="right" style="overflow: hidden">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```


2. 使用`table`

```html
<div class="demo5">
	<div class="parent" style="display: table; width: 100%">
		<div class="left" style="display: table-cell;width: 0.1%;padding-right: 20px;">
			<p style="width: 200px;">left</p>
		</div>
		<div class="right" style="display: table-cell;border-left: solid">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```


3. 使用`flex`

```html
<div class="demo5">
	<div class="parent" style="display: flex;">
		<div class="left" style="margin-right: 20px">
			<p style="width: 200px;">left</p>
		</div>
		<div class="right" style="flex: 1">
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```

## 等分多列布局

1. 使用`float + margin`。把`margin-left: -20px`去掉了

```html
<div class="demo6">
	<div class="parent clearfix" style="border: solid;overflow: auto;">
		<div class="column" style="float: left;width: 25%;padding-left: 20px;box-sizing: border-box;"><p>1</p></div>
		<div class="column" style="float: left;width: 25%;padding-left: 20px;box-sizing: border-box;border-left: solid"><p>2</p></div>
		<div class="column" style="float: left;width: 25%;padding-left: 20px;box-sizing: border-box;border-left: solid"><p>3</p></div>
		<div class="column" style="float: left;width: 25%;padding-left: 20px;box-sizing: border-box;border-left: solid"><p>4</p></div>
	</div>
</div>
```


2. 使用`table + margin`。把`margin-left: -20px`去掉了

```html
<div class="demo6">
	<div class="parent" style="display: table;width:100%;table-layout: fixed;">
		<div class="column" style="display: table-cell;padding-left: 20px;"><p>1</p></div>
		<div class="column" style="display: table-cell;padding-left: 20px;border-left: solid"><p>2</p></div>
		<div class="column" style="display: table-cell;padding-left: 20px;border-left: solid"><p>3</p></div>
		<div class="column" style="display: table-cell;padding-left: 20px;border-left: solid"><p>4</p></div>
	</div>
</div>
```


3. 使用`flex`

```html
<div class="demo6">	
	<div class="parent" style="display: flex;">
		<div class="column" style="flex: 1;"><p>1</p></div>
		<div class="column" style="flex: 1;margin-left:20px;border-left: solid"><p>2</p></div>
		<div class="column" style="flex: 1;margin-left:20px;border-left: solid"><p>3</p></div>
		<div class="column" style="flex: 1;margin-left:20px;border-left: solid"><p>4</p></div>
	</div>
</div>
```


## 等高多列布局

1. 使用`float + overflow`

```html
<div class="demo7">
	<div class="parent" style="overflow: hidden;">
		<div class="left" style="float: left; width: 100px;padding-bottom: 9999px;margin-bottom: -9999px;">
			<p>left</p>
		</div>
		<div class="right" style="overflow: hidden;padding-bottom: 9999px;margin-bottom: -9999px;border-left: solid;" >
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```


2. 使用`table`

```html
<div class="demo7">
	<div class="parent" style="display: table; width: 100%">
		<div class="left" style="display:table-cell; width: 100px;margin-right: 20px;">
			<p>left</p>
		</div>
		<div class="right" style="display:table-cell;border-left: solid" >
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```


3. 使用`flex`

```html
<div class="demo7">
	<div class="parent" style="display:flex">
		<div class="left" style="width: 100px;">
			<p>left</p>
		</div>
		<div class="right" style="flex:1;border-left: solid" >
			<p>right</p>
			<p>right</p>
		</div>
	</div>
</div>
```

# flex布局



# 圣杯布局

```html
<div id="shengbei" style="width: 500px; margin: 50px auto">
    <div style="height: 50px">header</div>
    <div style="padding: 0 100px;height: 200px">
        <div style="position: relative;float: left;width: 100%;height: 200px">
            main</br>
            自身与left、right是并排关系
        </div>
        <div style="position: relative;float: left;width: 100px;height: 200px;margin-left: -100%;left: -100px">
            left
        </div>
        <div style="position: relative;float: left;width: 100px;height: 200px;margin-left: -100px;right: -100px">
            right
        </div>
    </div>
    <div style="height: 50px">footer</div>
</div>
```

# 双飞翼布局

```html
<div id="bysf" style="width: 500px; margin: 50px auto">
    <div style="height: 50px;">header</div>
    <div style="height: 200px;width: 500px">
        <div style="float: left;width: 100%;">
            <div style="margin: 0 100px;height: 200px;">
                main</br>
                父元素与left、right是并列关系
            </div>
        </div>
        <div style="float: left;width: 100px;height: 200px;margin-left: -100%;">
            left
        </div>
        <div style="float: left;width: 100px;height: 200px;margin-left: -100px;">
            right
        </div>
    </div>
    <div style="height: 50px;">footer</div>
</div>
```