<template>
  <el-dialog title="JS逻辑编辑" :visible.sync="codeDialogVisible" width="70%" top="10vh" :before-close="handleClose"
    :center=true>
    <CodeEditor style="max-height: 65vh;" ref="codeEditor"></CodeEditor>

    <div style="text-align:center;padding: 10px;">
      <el-button type="primary" @click="onSave">确认修改</el-button>
      <div style="color: #6c6c6c; font-size:12px; margin-top:5px;">Tips: 确认修改之后将会影响最终生成的代码逻辑</div>
      <div v-if="error" style="color: red; font-size:12px; margin-top:5px;">请检查语法错误：{{error}}</div>
    </div>
  </el-dialog>

</template>

<script>
import CodeEditor from './CodeEditor.vue'

export default {
  props: ['codeDialogVisible'],
  components: {
    CodeEditor
  },

  data() {
    return {
      error: ''
    };
  },
  beforeCreate() { },
  created() { },
  beforeMount() { },
  mounted() { },
  beforeUpdate() { },
  updated() { },
  destoryed() { },
  methods: {
    // 在此自动生成
    request() {
      // 网络请求，可选
    },
    handleClose() {
      this.$emit("update:codeDialogVisible", false);
    },
    onSave() {
      const code = this.$refs.codeEditor.getEditorCode();
      // 去掉注释
      const temp = code.replace(/.+\*\/\s*/gs, "");
      try {
        // 转换为对象
        const JSCodeInfo = eval(`(function(){return ${temp}})()`);
        this.$emit("saveJSCode", JSCodeInfo);
        this.handleClose();
        this.error = '';
      } catch (error) {
        console.warn(error);
        this.error = error;
      }
    }
  },
  watch: {
  },
  computed: {
  },
  fillter: {},
};
</script>

<style scoped>
/*  在此自动生成 */

::v-deep .el-dialog__body {
  padding: 0 30px !important;
}
</style>