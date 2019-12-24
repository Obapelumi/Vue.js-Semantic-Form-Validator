<template>
  <form :id="id">
    <slot name="fields" :errors="validationErrors"></slot>
    <span @click.prevent="validateForm()">
      <slot name="submit"></slot>
    </span>
  </form>
</template>

<script>
export default {
  data: () => ({
    validationErrors: {}
  }),
  methods: {
    validateForm() {
      const formId = this.id;
      const errorObjectName = "validationErrors";
      var nodes = document.querySelectorAll(`#${formId} :invalid`);
      var vm = this; // current vue instance;

      Object.keys(this[errorObjectName]).forEach(key => {
        this[errorObjectName][key] = null;
      });

      if (nodes.length > 0) {
        nodes.forEach(node => {
          if (node.title) {
            this[errorObjectName][node.name] = node.title;
          } else {
            this[errorObjectName][node.name] = node.validationMessage;
          }

          node.addEventListener("change", function(e) {
            vm.validateForm(formId, errorObjectName);
          });
        });

        this[errorObjectName] = Object.assign({}, this[errorObjectName]);
        this.$emit("error", this.validationErrors);
        return false;
      } else {
        this.$emit("submit");
        return true;
      }
    }
  },
  props: ["id"]
};
</script>