<template>
  <div>
    <form id="custom-form">
      <div v-html="formHtml"></div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  props: {
    formData: {
      type: Object,
      defaut: function() {
        return {};
      }
    },
    formHtml: [String]
  },
  methods: {
    setValue(element, value) {
      switch (element.type) {
        case "radio":
          if (value == "on") {
            element.checked = true;
          } else {
            if (element.value == value) {
              element.checked = true;
            }
          }
          break;
        case "checkbox":
          if (value == "on") {
            element.checked = true;
          } else {
            if (value instanceof Array) {
              for (var i = 0; i < value.length; i++) {
                const v = value[i];
                if (element.value == v) {
                  element.checked = true;
                }
              }
            } else {
              if (element.value == value) {
                element.checked = true;
              }
            }
          }
          break;
        case "select-one":
          for (var i = 0; i < element.length; i++) {
            if (element.options[i].value == value) {
              element.selectedIndex = i;
            }
          }
          break;
        case "select-multiple":
          for (var i = 0; i < element.length; i++) {
            if (
              value.findIndex(item => item == element.options[i].value) > -1
            ) {
              element.options[i].selected = true;
            } else {
              element.options[i].selected = false;
            }
          }
          break;
        case "text":
        case "textarea":
        case "hidden":
          element.value = value;
          break;
      }
    }
  },
  mounted() {
    var form = document.forms["custom-form"];

    for (const key in this.formData) {
      if (this.formData.hasOwnProperty(key)) {
        const value = this.formData[key];
        var el;
        if (value instanceof Array) {
          el = form.elements[`${key}[]`] || form.elements[key];
        } else {
          el = form.elements[key];
        }
        if (el) {
          if (el instanceof RadioNodeList) {
            if (el.length) {
              for (var i = 0; i < el.length; i++) {
                const element = el[i];
                this.setValue(element, value);
              }
            } else {
              this.setValue(el, value);
            }
          } else {
            this.setValue(el, value);
          }
        }
      }
    }
  }
};
</script>

<style>
</style>
