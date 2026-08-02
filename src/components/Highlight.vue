<template>
  <div class="highlight-box">
    <slot></slot>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.highlight-box {
  border: 3px solid orange;
  padding: 20px;
  border-radius: 8px;
}
</style>