# CSS清楚浮动的意义

## 正方形

## 普通正方形

- 直接定宽高

## 自适应正方形

有三种方法：

1. 用css3的新单位 vh、vw
2. padding-bottom = width = 某百分比
	- 缺点1：不能有文字填充
	- 缺点2：由于该块状元素没有高度，因为设置`max-height`失效
3. 利用伪类来撑开父容器，父容器设置为某百分比后，添加一个伪类设置`margin-top: 100%`。注意，由于`margin-collapse(外边距塌陷)`的问题，
	- 缺点：内部仍然无法包含文字。但是可以设置`max-height`
	
## 三角形
	
	
	