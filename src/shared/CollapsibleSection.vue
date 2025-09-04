<template>
    <div>
        <div class="header">
            <span v-if="open" @click="open = !open">&#x25B2; Collapse</span>
            <span v-if="!open" @click="open = !open">&#x25BC; Expand</span>
        </div>
        <slot v-if="open">
        </slot>
    </div>
</template>

<script>
export default {
  name: 'CollapsibleSection',
  data() {
    return {
      open: true,
    };
  },
};
</script>

<style scoped>
.header {
  background-color: #ff94ad;
  color: white;
  padding: 5px;
  cursor: pointer;
  user-select: none;
}
</style>