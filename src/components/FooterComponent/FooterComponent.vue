<template>
  <footer class="footer">
    <div class="socials">
      <p>STAR WARS WORLD SOCIALS:</p>
      <ul>
        <li><i class="bx bxl-facebook-circle"></i></li>
        <li><i class="bx bxl-instagram"></i></li>
      </ul>
    </div>
    <div class="streck"></div>
    <div class="about">
      <h3>About:</h3>
      <p>
        We are 2 students Dhan and Luisa who are in their final year of newton competence education. During one of our courses' development of web applications. We were given a task of creating a vue app that uses the star wars api to retrieve information to the user. Our goal was to create a user friendly page for our star wars nerds where they can easily find information on various characters or movies.

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