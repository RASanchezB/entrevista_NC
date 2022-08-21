<template>
  <div class="nav">
    <a href="#">Home</a>
    <a href="#">Other Page</a>
  </div>
</template>


<script>
export default {
  name: 'HeaderItem',
}
</script>


<style>
.nav{
  background-color: green;
  overflow: hidden;
  width: 100%;
  align-content: center;
}
.nav a{
  color: white;
  float: left;
  text-align: center;
  padding: 15px 15px;
  font-size: 16px;
  text-decoration: none;
  margin: 5px;
  align-content: center;
  position: relative;
  margin-left: 25%;
}
</style>
