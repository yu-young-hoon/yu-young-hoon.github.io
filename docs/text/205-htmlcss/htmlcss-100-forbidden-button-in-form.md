---
layout: default
title: HTML/CSS div 또는 form으로 table 만들기
parent: htmlcss
nav_order: 205100
---

## CSS 부분
```css
DIV.table 
{
    position: absolute;
    top:50px;
    display:table;
    border-style: solid; 
    border-color: #969696; 
    border-width: 1px 0 0 1px;
}

FORM.tr, DIV.tr
{
    display:table-row;
}

SPAN.td
{
    padding: 5px;
    display:table-cell;
    border-style: solid;
    border-color: #969696;
    border-width: 0 1px 1px 0;
}
```

## html 부분
```html
<div class="table" style="">  
	<div class="tr">
		<span class="td">이름</span>
		<span class="td">아이디</span>
	</div>
	<form action="/admin" method="post" class="tr">
		<span class="td">simuruk</span>
		<span class="td">wiki</span>
	</form>
</div>
```
