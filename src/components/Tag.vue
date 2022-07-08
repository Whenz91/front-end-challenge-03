<script setup>

</script>

<template>
  <div class="tag">
    <slot></slot>
  </div>
</template>


<style scoped>
.tag {
    width: max-content;
    border: 1px solid var(--c-black-soft);
    color: var(--c-black-soft);
    text-transform: uppercase;
    font-weight: 700;
    font-size: 12px;
    padding: 7px 10px;
    border-radius: 12px;
}
</style>