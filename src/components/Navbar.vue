<template>
  <div class="navbar">
    <div class="content">
      <div class="left">
        <img src="../assets/Logos/d4g.png" alt="" class="d4G" />
      </div>
      <div class="mid">
        <img src="../assets/Logos/sogre.png" alt="" class="logo" />
      </div>
      <div class="right">
        <li>Ruben Chetboun</li>
        <li>Romain Charrat</li>
        <li>Lounis Sofiane</li>
      </div>
    </div>
  </div>
</template>


      
      

<script>
export default {};
</script>

<style>
.navbar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 80px;
}
.content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 80%;
}
.right {
  width: 20%;
}
li {
  font-size: 0.8em;
  color: white;
}
img {
  width: 150px;
  height: auto;
}
</style>