<template>
  <div class="row">
    <div class="d-flex justify-content-center" >
      <div class="card" style="width: 90%;">
        <div class="card-header fw-bolder" style="text-align: center;">HTMl kod editörü</div>
        <div class="card-body">
          <div class="container">
          <div class="d-flex flex-row col-12 flex-wrap">
            <div class="col-6 p-2" ><textarea ref="editor" v-model="editorContent"></textarea></div>
            <div class="col-6 p-2"><div class="output" v-html="htmlCode"></div></div>
          </div>
        </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onMounted, defineComponent } from 'vue';
import 'codemirror/lib/codemirror.css';
import 'codemirror/mode/htmlmixed/htmlmixed';
import CodeMirror from 'codemirror';

export default defineComponent({
  name: 'home',
  components:{},

  setup() {
    const editorContent = ref('');
    const htmlCode = ref('');

    onMounted(() => {
      const editor = CodeMirror.fromTextArea(
        document.querySelector('textarea'),
        {
          mode: 'htmlmixed',
          theme: 'default',
          lineNumbers: true,
          value: editorContent.value
        }
      );

      editor.on('change', () => {
        editorContent.value = editor.getValue();
        htmlCode.value = editorContent.value;
      });
    });

    return {
      editorContent,
      htmlCode
    };
  }
});
</script>

<style>
.output {
  margin-top: 20px;
  border: 1px solid #ccc;
  padding: 10px;
  height: 85vh;
}
</style>
