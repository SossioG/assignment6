<script setup>

</script>

<template>
    <div class="header">
        <img alt="Vue logo" class="logo" src="/favicon.ico" width="125" height="125" />
        <div class="wrapper">
            <h4>Min filmlista</h4>
        </div>
    </div>
</template>

<style scoped>
  /* MAIN */
  .header {
    position: absolute;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    line-height: 1.5;
    background: white;
  }


  .logo {
    height: 60px;
    width: 60px;
    margin: 0 auto 2rem;
  }

  /* MEDIA */
  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      padding-right: calc(var(--section-gap) / 2);
    }

    .logo {
      margin: 0 2rem 0 0;
    }

  }
</style>