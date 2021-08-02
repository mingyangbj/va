<template>
  <div class="view-auto"></div>
  <div class="view-px"></div>

</template>

<script>

export default {
  name: 'App',
  components: {

  }
}
</script>

<style lang="scss">
@import './styles/view-auto-adapte';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.view-auto{
  width: va(100);
  height: va(100);
  background: #42b983;
}

.view-px{
  margin-top: 50px;
  width: 100px;
  height: 100px;
  background: #42b983;
}

</style>
