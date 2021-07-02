<template>
  <main>
    <h1>koke0702_ バーナー</h1>
  </main>
</template>

<script>
export default {}
</script>

<style scoped>
  main{
    padding: 10rem;
    background-color: #0ff;
  }
  h1{
    color: #f00;
    font-size: 5vw;
    animation: infinite alternate-reverse 0.2s unco;
  }  
  @keyframes unco {
    0%{
      transform: translateX(500px);
    }
    
    100%{
      transform: translateX(-500px);
    }
  }
</style>