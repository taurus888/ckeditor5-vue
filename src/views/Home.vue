<template>
  <div class="home">
    <div id="editor">
      <ckeditor :editor="editor" @ready="onReady" v-model="editorData" :config="editorConfig">

      </ckeditor>
    </div>

    <button v-on:click="emptyEditor()">清空内容</button>

  </div>
</template>

<script>
import DecoupledDoc from '@ckeditor/ckeditor5-build-decoupled-document';
import '@ckeditor/ckeditor5-build-decoupled-document/build/translations/zh-cn' //中文包
const upload = require('../assets/upload')

export default {
  name: 'home',
  data(){
    return{
      editor: DecoupledDoc,
      editorData: '<h1>文档型富文本编辑器</h1>',
      editorConfig: {
        // 编辑器的配置
        language: 'zh-cn',  // 中文
        extraPlugins: [ upload.MyCustomUploadAdapterPlugin ],
      }
    }
  },
  created(){
  },
  methods:{
    onReady( editor )  {
      // 在可编辑区域之前插入工具栏。
      editor.ui.getEditableElement().parentElement.insertBefore(
              editor.ui.view.toolbar.element,
              editor.ui.getEditableElement()
      );

    },
    emptyEditor() {
      this.editorData = '';
    }
  },

}
</script>
<style>
  .ck-editor__editable {
    min-height: 400px;
    border: 1px solid #ccc!important;
  }
</style>
