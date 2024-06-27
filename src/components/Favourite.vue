<template>
  <h2>Varients of favourites</h2>
  <div v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>
<script>
export default {
  data() {},

  props: {
    favs: {
      type: Array,
      require: true,
    },
  },
};
</script>
<style scoped>
h2 {
  color: azure;
}
div{
    display: flex;
    justify-content: space-between;
    width: 500px;
    margin:  10px auto;
    transition: all 500ms ease;
}
span{
    padding: 10px 15px;
    background: #fff;
    color:black;
}
div:hover{
    opacity: 0.7;
    transform: scale(1.1);
    cursor: pointer;
}
</style>
