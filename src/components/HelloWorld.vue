<template>
  <div>
    <ckeditor v-model="formData.floorText"
              :editor="editor"
              :config="editorConfig"
              @ready="onReady" />
  </div>
</template>

<script>
import DecoupledEditor from '@ckeditor/ckeditor5-build-decoupled-document'
import CKEditor from '@ckeditor/ckeditor5-vue'
import '@ckeditor/ckeditor5-build-decoupled-document/build/translations/zh-cn.js'
export default {
  components: {
    ckeditor: CKEditor.component
  },
  data () {
    return {
      formData: {},
      editorConfig: {
        removePlugins: ['MediaEmbed'],
        language: 'zh-cn',
        ckfinder: {
          'uploaded': 1,
          'url': '/'
        },
        // plugins: [Autoformat, Table, TableToolbar, PasteFromOffice],
        toolbar: [
          'heading',
          'fontSize',
          'highlight',
          'fontFamily',
          'alignment',
          'imageUpload',
          'insertTable',
          'bold',
          'underline',
          'increaseIndent',
          'decreaseIndent',
          'bulletedList',
          'numberedList',
          'imageStyle:full',
          'imageStyle:alignLeft',
          'imageStyle:alignRight',
          'undo', 'redo'
        ],
        fontSize: {
          options: [14, 16, 'default', 20, 22, 24, 26, 28, 32, 48]
        },
        fontFamily: {
          options: ['宋体', '仿宋', '微软雅黑', '黑体', '仿宋_GB2312', '楷体', '隶书', '幼圆']
        },
        table: {
          contentToolbar: ['tableColumn', 'tableRow', 'mergeTableCells']
        },
        // indentBlock: {
        //     offset: 2,
        //     unit: 'em'
        // }
        borderStyle: "black"
      },
      editor: DecoupledEditor,
    }
  },
  methods: {
    onReady (editor) {
      editor.ui.getEditableElement().parentElement.insertBefore(
        editor.ui.view.toolbar.element,
        editor.ui.getEditableElement()
      )
      editor.plugins.get('FileRepository').createUploadAdapter = loader => {
        return {
          upload: async () => {
            return await loader.file.then(f => {
              const F = new FileReader()
              // F.readAsArrayBuffer(f);
              F.readAsDataURL(f)
              return new Promise(resolve => {
                F.onload = function () {
                  resolve({ bufAsArray: F.result.split(',')[1], file: f })
                }
              })
            }).then(v => {
              console.log('v', v)
              // 执行上传上传
              return this.uploadImgHook(v)
              // 返回标准格式
              /* return {
                default: 'http://mmcl.maoming.gov.cn/ys/css/img/BG.png'
              }*/
            })
          }
        }
      }
    }
  }
}
</script>