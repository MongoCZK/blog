### CSS作用域

当style标签有scoped属性时，它的CSS只作用于当前组件中的元素。它通过使用PostCSS来实现以下转换

```HTML
<style scoped>
.example {
  color: red;
}
</style>

<template>
  <div class="example">hi</div>
</template>
```

转换结果

```html
<style>
.example[data-v-f3f3eg9] {
  color: red;
}
</style>

<template>
  <div class="example" data-v-f3f3eg9>hi</div>
</template>
```

 vue组件中`<style>`标签加上`scoped`属性时，会在组件中的每个元素上（如果有子组件，则只在子组件的根节点上添加属性）添加唯一的属性（data-v-hash）,css编译后也会加上属性选择器，从而达到限制作用域的目的

`scoped`作用原理可概括为以下几点：

+ 给HTML的DOM节点加一个不重复的data属性（data-v-hash）来表示它的唯一性

+ 在每条css规则的选择器的末尾（编译后生成的css语句）加上当前组件的data属性值选择器（如 [data-v-hash] ）来私有化样式
+ 如果组件内部包含有其他组件，只是给其他组件的根节点加上data属性

### 子组件的根元素

使用``scoped`后，父组件的样式将不会渗透到子组件中。不过一个子组件的根节点会同时受其父组件有作用域的CSS和子组件有作用域的CSS的影响。这样设计是为了让父组件可以从布局的角度出发，调整其子组件根元素的样式

### 深度选择器

如果想要`scoped`样式中的一个选择器能够作用得更深，例如影响子组件，可以使用 `>>>` 操作符（仅适用于CSS）：

```html
<style scoped>
.a >>> .b { 
	color: red;    
}
</style>
```

上述代码会编译成

```html
<style>
.a[data-v-f3f3eg9] .b { 
	color: red;
}
</style>
```

如需支持sass/less预处理器，可使用`/deep/`, `::v-deep`

```html
<style lang="scss" scoped>
.a /deep/ .b { 
	color: red;    
}
.a ::v-deep .b { 
	color: red;    
}
</style>
```

`/deep/`在vue3.0中会报错，需要使用`::v-deep`