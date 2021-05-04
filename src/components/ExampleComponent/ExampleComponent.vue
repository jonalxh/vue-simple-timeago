<template>
    <div class="SimpleTimeAgo" :style="{color}">
        <slot></slot>
    </div>
</template>

<script>
  export default {
    name: 'SimpleTimeAgo',
    props: {
      color: {
        type: String,
        default: 'red'
      }
    }
  }
</script>
