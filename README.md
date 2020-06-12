# customized-form-preview

自定义表单预览，表单数据绑定

`npm i customized-form-preview`

```javascript
<template>
  <CustomizedFormPreview id="my-form-name" :formData="formData" :formHtml="formHtml" />
</template>
<script>
import CustomizedFormPreview from "customized-form-preview";
export default {
  data() {
    return {
      formData: {mycheckbox:'a'},
      formHtml: '<input type="checkbox" name="mycheckbox" value="a"/>'
    };
  },
  components: {
    CustomizedFormPreview
  }
}
</script>
```

```javascript
  props: {
    formData: {
      type: Object,
      defaut: function() {
        return {};
      }
    },
    formHtml: [String],
    buttonText: { type: String, default: "" }, // 按钮文字，不设置则不出现按钮
    save: Function //回调方法 也可在父组件调用子组件的handleClick来获取数据，如： this.$refs.form2.handleClick();
  },
```
