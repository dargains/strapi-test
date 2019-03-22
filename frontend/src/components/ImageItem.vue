<template lang="html">
  <li>
    <h2>{{title}}</h2>
    <p>{{description}}</p>
    <figure>
      <img :src="source" :alt="title">
    </figure>
  </li>
</template>

<script>
export default {
  props: ['title', 'description', 'source']
}
</script>

<style lang="css" scoped>
li {
  padding: 20px;
}
figure {
  max-width: 400px;
}
img {
  width: 100%;
}
</style>
