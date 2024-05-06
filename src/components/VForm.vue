<template>
  <div>
    <v-form>
      <component
        :is="componentName"
        v-for="(component, index) in formComponents"
        :key="index"
        :textFieldProps="component"
      ></component>
      <v-btn color="primary" @click="handleSubmit">{{ buttonProps.text }}</v-btn>
    </v-form>
  </div>
</template>

<script>
import VTextField from "./VTextField.vue";

export default {
  components: {
    VTextField,
  },
  props: {
    formComponents: {
      type: Array,
      required: true,
    },
    buttonProps: {
      type: Object,
      required: true,
    },
  },
  computed: {
    componentName() {
      return "VTextField";
    },
  },
  methods: {
    handleSubmit() {
      // Add your form submission logic here
      console.log("Form submitted");
    },
  },
};
</script>
