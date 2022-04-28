<template>
  <div class="container">
    <router-link :to="{ name: 'fruit.index' }">List Fruit</router-link>
    <router-view></router-view>
  </div>
</template>

<script>
export default {};
</script>
