### 安装tailwind css
```shell
npm install tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

### 创建配置文件
```shell
npx tailwindcss init -fill
```

### 在项目根目录下创建postcss.config.js文件
```JavaScript
// postcss.config.js
module.exports = {
  purge: [],
  darkMode: false,
  theme: {
    extend: {}
  },
  variants: {},
  plugins:[]
}
```

### 在main.js中引入tailwind css
```javascript
import "tailwindcss/tailwind.css"
```

### 使用
[参考手册](https://www.tailwindcss.cn/docs/preflight)