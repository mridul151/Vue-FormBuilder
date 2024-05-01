<template>
  <v-text-field
    :value="value"
    :label="label"
    :placeholder="placeholder"
    @input="$emit('input', $event)"
  ></v-text-field>
</template>

<script>
export default {
  name: 'VTextField',
  props: {
    label: {
      type: String,
      default: ''
    },
    placeholder: {
      type: String,
      default: ''
    },
    value: {
      type: String,
      default: ''
    }
  }
}
</script>
