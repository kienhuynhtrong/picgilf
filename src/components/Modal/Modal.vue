<template>
  <transition name="modal">
    <div class="modal-mask" @click="$emit('close')">
      <div class="modal-wrapper">
        <div class="modal-container">
          <img :src="src">
          <button class="modal-default-button" @click="$emit('close')">Close</button>
        </div>
      </div>
    </div>
  </transition>
</template>
<script>

export default {
    name:'Modal',
    props: {
      src: String
    },
    methods: {
      closed() {
        this.$emit('close')
      },

      opened() {
        this.$emit('opened');
      },
    }
}
</script>
<style lang='scss' src='./modal.scss'>
</style>