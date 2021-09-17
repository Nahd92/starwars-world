<template>
  <footer class="footer">
    <div class="socials">
      <p>STAR WARS WORLD SOCIAL:</p>
      <ul>
        <li><i class="bx bxl-facebook-circle"></i></li>
        <li><i class="bx bxl-instagram"></i></li>
      </ul>
    </div>
    <div class="streck"></div>
    <div class="about">
      <h3>About:</h3>
      <p>
        Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod
        tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim
        veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea
        commodo consequat. Duis aute irure dolor in reprehenderit in voluptate
        velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint
        occaecat cupidatat non proident, sunt in culpa qui officia deserunt
        mollit anim id est laborum.
      </p>
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


.footer {
  
  text-align: center;
  height: 20em;
  background-color: var(--dark-color);
}
.socials {
  padding-top: 3em;
}
.about {
  text-align: center;
  margin-top: 1em;
  margin-bottom: 0px;
}
.footer ul {
  display: flex;
  justify-content: center;
}
.footer ul li i {
  cursor: pointer;
  font-size: 2em;
  padding: 8px;
}
.footer ul li i:hover {
  box-shadow: 0 0 10px 2px rgba(252, 248, 248, 0.2);
  border-radius: 80%;
}
@media screen and (min-width: 900px) {
  .footer {
 display: flex;
 flex: wrap;
 justify-content: space-around;
  background-color: var(--dark-color);
}
.socials{
  flex:70%;
  padding: 5em;
}
.socials ul{
  display: flex;
  padding: 1em;
}
.socials ul li i{
  font-size:2em;
  padding-left: 0.2em;
}
.streck{
  background-color:grey ;
  width:0.2em;
  opacity: 50;
  height: 18em;
  margin-top:2em;
}
.about{
  padding: 5em;
  text-align: left;
}
}

</style>