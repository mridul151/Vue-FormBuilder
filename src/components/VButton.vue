<template>
  <v-btn
    :color="color"
    :outlined="outlined"
    @click="$emit('click')"
  >
    {{ buttonText }}
  </v-btn>
</template>

<script>
export default {
  name: 'VButton',
  props: {
    color: {
      type: String,
      default: 'primary'
    },
    outlined: {
      type: Boolean,
      default: false
    },
    buttonText: {
      type: String,
      default: 'Button'
    },
    // New prop for the text on the button
    text: {
      type: String,
      default: 'Button Text'
    }
  }
}
</script>
