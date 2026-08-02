<template>
  <div class="slot-wrapper">
    <slot></slot>
  </div>

</template>

<script>
export default {
  data() {
    return {
      clyk: 0
    }
  },
  methods: {
    addClyk() {
      this.clyk++;
    }
  }
}
</script>
<style scoped>
.slot-wrapper {
  border: blueviolet 2px solid;
  border-radius: 3px;
  margin-bottom: 20px;
  padding: 5px;
}
</style>