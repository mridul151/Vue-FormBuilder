<template>
  <v-text-field
    :value="value"
    :label="label"
    :type="type"
    :outlined="outlined"
    @input="handleInput"
  ></v-text-field>
</template>

<script>
export default {
  name: 'VTextField',
  props: {
    label: {
      type: String,
      default: 'Text Field'
    },
    type: {
      type: String,
      default: 'text'
    },
    outlined: {
      type: Boolean,
      default: true
    },
    value: {
      type: String,
      default: ''
    }
  },
  methods: {
    handleInput(event) {
      const newValue = event.target.value;
      if (newValue !== this.value) {
        this.$emit('input', newValue);
      }
    }
  }
}
</script>
