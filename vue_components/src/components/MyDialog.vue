<template>
  <div class="dialog" v-if="isShowDialog === true" @click="hideDialog">
    <div class="dialog__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    isShowDialog: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    hideDialog() {
      this.$emit('update:isShowDialog', false)
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0,0,0,0.6);
  position: fixed;
  display: flex;
}

.dialog__content {
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300px;
  padding: 20px;
}
</style>