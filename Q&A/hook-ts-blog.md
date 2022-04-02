## 创建

- ```bash
  npx create-react-app hook-ts-blog --template typescript
  ```





## Antd

- ```
  //安装依赖
      "babel-plugin-import": "^1.13.0",	//按需导入
      "customize-cra": "^1.0.0",	//react-app-rewired的依赖
      "react-app-rewired": "^2.1.6",	//可以修改配置
  ```

- ```
  //新建config-overrides.js
  const { override, fixBabelImports } = require('customize-cra')
  
  module.exports = override(
    fixBabelImports('import', {
      libraryName: 'antd',
      libraryDirectory: 'es',
      style: 'css'
    })
  )
  ```

- ```
  //package.json中修改
    "scripts": {
      "start": "react-app-rewired start",
      "build": "react-app-rewired build",
      "test": "react-app-rewired test",
      "eject": "react-scripts eject"
    },
  ```

- 这样在组件中就可以import { DatePicker } from 'antd';按需引入且不需要引入css



## CSS

- @emotion/core







## Router

- @reach/router
- @types/reach__router























