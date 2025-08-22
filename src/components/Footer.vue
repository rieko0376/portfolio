<template>
  <footer>
    <p class="copyright">@2025　Miyamoto</p>
  </footer>
</template>

<style scoped>
footer{
  background-color: var(--green);
  width: 100%;
  height: auto;
  padding: 3vw 0.5rem;
}

.copyright{
  font-size: var(--txt_min_sp);
  color: #fff;
}

/* PC版　*/
@media (min-width:1024px){
  footer{
    padding: 20px 0.5rem;
  }

  .copyright{
    font-size: var(--txt_min_pc);
  }
}
</style>