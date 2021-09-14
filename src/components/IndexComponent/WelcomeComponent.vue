<template>
  <div class="welcome">
    <div class="welcome-container">
      <img
        src="../../assets/star.png"
        alt="White Helmet"
        class="white-helmet"
      />
      <div class="welcome-text">
        <h1>STAR WARS WORLD</h1>
        <p>Welcome to star wars world!</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "WelcomeComponent",
};
</script>

<style lang="scss" >
.welcome {
  .welcome-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 5em;

    .white-helmet {
      margin-top: 4em;
      width: 60%;
    }

    .welcome-text {
      padding: 0 2.5em;
      font-size: 1em;
      text-shadow: 0 -1px 0 #fff, 0 1px 0 #2e2e2e, 0 2px 0 #2c2c2c,
        0 3px 0 #2a2a2a, 0 4px 0 #282828, 0 5px 0 #262626, 0 6px 0 #242424,
        0 7px 0 #222, 0 8px 0 #202020, 0 9px 0 #1e1e1e, 0 10px 0 #1c1c1c,
        0 11px 0 #1a1a1a, 0 12px 0 #181818, 0 13px 0 #161616, 0 14px 0 #141414,
        0 15px 0 #121212, 0 22px 30px rgba(0, 0, 0, 0.9);
    }
    .welcome-text p {
      font-size: 0.8em;
      text-align: center;
      padding: 0 1.5em;
      color: #fff;
    }
  }
}

@media screen and (min-width: 727px) {
  .welcome {
    .welcome-container {
      margin: 0;
      padding: 0;
      .white-helmet {
        width: 50%;
      }
      .welcome-text {
        text-align: center;
        font-size: 0.7em;
        letter-spacing: 0.02em;
      }
      .welcome-text p {
        font-size: 0.7em;
        text-align: center;
      }
    }
  }
}

@media screen and (min-width: 1024px) {
  .welcome {
    .welcome-container {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      margin-top: 2em;
      .white-helmet {
        display: block;
        width: 32%;
      }
      .welcome-text {
        text-align: center;
        font-size: 2.5em;
        letter-spacing: 0.02em;
      }
      .welcome-text p {
        font-size: 0.5em;
        text-align: center;
      }
    }
  }
}
</style>