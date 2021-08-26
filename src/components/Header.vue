<template>
  <header>
      <img src="@/assets/img/logo.png" alt="">
  </header>
</template>

<script>
export default {
    name:'Header',

}
</script>

<style scoped lang="scss">
header{
    display: flex;
    // flex-grow: 1;
    width: 100vw;  
    justify-content: center;
    align-items: center;
    background-color: #0D0F8D;
    img{
        display: block;
        width: 200px;
        height: auto;
        margin: 40px;
    }
}
</style>