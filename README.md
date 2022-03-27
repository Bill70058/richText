# rich-text

## ckeditor使用
vue2.x环境下富文本编辑器ckeditor使用
需要下载五个依赖，对应的版本号也有要求，最新的版本是vue3.x的

### 下载
> 将以下这段复制到package.json并npm install

```json
"@ckeditor/ckeditor5-autoformat": "^16.0.0",
"@ckeditor/ckeditor5-build-decoupled-document": "^12.4.0",
"@ckeditor/ckeditor5-paste-from-office": "^16.0.0",
"@ckeditor/ckeditor5-table": "^16.0.0",
"@ckeditor/ckeditor5-vue": "^1.0.0",
```
### 使用
- v-model：需要绑定一个``v-model``作为富文本输出的变量
- editor：需要绑定一个编辑器，由依赖``@ckeditor/ckeditor5-build-decoupled-document``导出
- config：配置富文本编辑器展示的工具区内容
- onReady：初始化富文本编辑器，简单使用复制模板的即可

### 运行示例
```
npm install
npm serve
```