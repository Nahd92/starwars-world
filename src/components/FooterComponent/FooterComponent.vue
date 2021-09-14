<template>
  <footer class="footer">
   
    <p>STAR WARS WORLD SOCIAL:</p>
    <ul>
      <li> <i class='bx bxl-facebook-circle'></i></li>
      <li> <i class='bx bxl-instagram'></i></li>
    </ul>
    <div class="about">
      <h3>About:</h3>
      <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.</p>
    </div>
  </footer>
  
</template>

<script>
export default {
  name: "FooterComponent",
};
</script>

<style lang="scss" scoped>
@import "./style/styles.scss";


.footer{
  text-align: center;
  height: 20em;
  background-color: var(--dark-color);

}

.about{
  text-align: center;
  margin-top:1em;
  margin-bottom:0px;
}
.footer ul{
  display: flex;
  justify-content: center;
  
}
.footer ul li i{
  font-size: 2em;
  padding:8px;
  
}
</style>