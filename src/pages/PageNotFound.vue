<template>
  <div class="col-full">
    <h1 class="headingLarge">Not found </h1>
    <p class="textLarge">
      Ooops, we couldn't find what you are looking for. Why don't you 
      <router-link :to="{name: 'Home'}">go home instead</router-link>
    </p>
  </div>
</template>

<script>
export default {
}
</script>

<style scoped>
.headingLarge {
  font-size: 100px;
}
.textLarge {
  font-size: 50px;
  font-weight: 100;
}
.centered {
  text-align: center;
}
</style>
