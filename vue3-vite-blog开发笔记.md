1. 创建typescript模板的vue3项目：

   ```yarn create @vitejs/app my-vue-app --template vue-ts```

2. vue3 element plus按需引入：

   ```yarn add element-plus```

   ```npm i vite-plugin-style-import vite-plugin-components -D```

   ```js
   //vite.config.js
    
   import styleImport from 'vite-plugin-style-import'
   import ViteComponents, { ElementPlusResolver } from 'vite-plugin-components'
    
   export default defineConfig({
       plugins: [
           vue(),
           //按需导入element-plus组件
           ViteComponents({
               customComponentResolvers: [ElementPlusResolver()],
           }),
           //按需导入element-plus的css样式
           styleImport({
               libs: [
                   {
                       libraryName: 'element-plus',
                       esModule: true,
                       resolveStyle: name => {
                           return `element-plus/lib/theme-chalk/${name}.css`
                       },
                   },
               ],
           }),
   
   ```

   

3. 使用antd的样式按需引入，参考文档官网3.x

