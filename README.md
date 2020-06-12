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
