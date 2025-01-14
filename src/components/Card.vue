<script setup lang="ts">
type Props = {
  bgColor?: string
}

withDefaults(defineProps<Props>(), {
  bgColor: 'bg-gray-100',
})
</script>

<!--
<slot></slot> is a special component in Vue that allows you to render content inside a component.
It's working like {children} in React.
-->

<template>
  <div :class="`${bgColor} p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>
