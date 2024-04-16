<template>
  <section class="min-vh-100 d-flex align-items-center">
    <div class="logo-container">
      <img src="/src/assets/logoSteelSaviorimg.png" alt="Logo">
    </div>
  </section>
  <section>
   
  </section>
</template>

<style scoped>

img{
  width: 80%;
}

.logo-container {
  position: relative;
  animation: fallAndBounce 1s ease forwards;
}

@keyframes fallAndBounce {
  0% {
    top: -650px;
  }
  50% {
    top: 50vh; 
    transform: translateY(-50%);
  }
  100% {
    top: 0; 
  }
}
</style>
