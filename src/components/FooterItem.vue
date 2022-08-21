<script>
export default {
  name: 'FooterItem',
}
</script>

<template>
  <div class="footer">
    <p class = "rights">
      Hecho por Ricardo Sanchez
    </p>
    <p class = "reservado">
      All rights reserved
    </p>
  </div>
</template>

<style scoped>
.footer{
  background-color: lightblue;
  overflow: hidden;
  height: 75px;
  margin: auto;
  position: relative; 
  width: 100%;
  bottom: 0%;
}
.rights{
  float: left;
  color: black;
}
.reservado{
  float: right;
  color: black;
}
</style>
