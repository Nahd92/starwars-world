<template>
    <section>
        <h2 class="character-title">All Character</h2>
        <div class="character-container">
            <div class="character-card">
                <div class="character-img">
                    <img src="../../assets/luke2.jpg" alt="luke">
                </div>
                <div class="character-information" >
                    <h3 class="character-name" >{{characterName}}</h3>
                    <h3 class="character-age">{{characterAge}}</h3>
                    <h3 class="character-eyes">{{characterEyeColor}}</h3>
                </div>
                <div class="card-button">
                    <button class="read-more">Reade more</button>
                </div>
            </div>
           
             
        </div>
        
    </section>
</template>
<script>

export default {
    name:"CharacterListComponent",
    data:()=> ({
        character:[],
        characterImages: {},
        dataFromapi:[]
        
    }),
    computed:{
        characterName(){
             return this.dataFromapi ? this.dataFromapi.name : ''
             

            
         },
        
        
        characterAge(){
           return this.dataFromapi ? this.dataFromapi.birth_year : ''
        },
        characterEyeColor(){
            return this.dataFromapi ? this.dataFromapi.eye_color : ''
        }

    },
   
    async mounted(){
        const url ="https://swapi.dev/api/people";
        try{
            const response = await fetch(url);
            const data = await response.json();
          this.dataFromapi = data
            
            for(let i=0; i<data.length; i++)
            {
                this.dataFromapi = data[i]


            }
            
          
           
        }
        catch(error)
        {
            console.log(error)
        }
    }
}
</script>
<style lang="scss" scoped>
@import "./style/styles.scss";

h3,
p {
  color: black;
}

.cards-overlay {
  position: absolute;
  height: 100vh;
  margin-top: 40em;
  width: 50%;
  background-color: var(--dark-color);
}



.character-title {
  text-align: center;
}

.character-title {
  font-size: 3em;
}
.character-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  align-items: center;
  justify-content: space-around;
  margin-top: 3em;
  height: 30em;
  overflow: hidden;

  .character-card {
    background-color: black;
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 17em;
    height: 25em;
    margin: 1em 1em;
    border-radius: 0.5em;
    -webkit-box-shadow: 2px 5px 16px 0px #0b325e,
      50px 50px 50px 50px rgba(145, 145, 145, 0),
      50px 50px 50px 50px rgba(145, 145, 145, 0);
    box-shadow: 2px 5px 16px 0px #0b325e,
      50px 50px 50px 50px rgba(145, 145, 145, 0),
      50px 50px 50px 50px rgba(145, 145, 145, 0);

    .character-img {
      background-color: var(--white-color);
      width: 94%;
      margin: 0.5em 0;

      img {
        border-radius: 0.5em;
        width: 17em;
        height:11em ;

      }
    }

    .character-information {
      text-align: center;
      width: 100%;
      margin-top: 2em;

      h3 {
        font-size: 1em;
        font-weight: normal;
        color: white;
      }
    }

    &:hover {
      -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
        2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
      box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
        5px 5px 15px 5px rgba(0, 0, 0, 0);
      transform: scale(1.1);
    }

    .card-button {
      margin-top: 2.5em;

      .read-more {
        font-size: 1.2em;
        padding: 0.7em;
        border-radius: 1em;
        background: rgba(31, 135, 255, 0.7);
        color: white;

        &:hover {
          -webkit-box-shadow: inset -1px 3px 8px 5px #1f87ff,
            2px 5px 16px 0px #0b325e, 5px 5px 15px 5px rgba(0, 0, 0, 0);
          box-shadow: inset -1px 3px 8px 5px #1f87ff, 2px 5px 16px 0px #0b325e,
            5px 5px 15px 5px rgba(0, 0, 0, 0);
          transform: scale(1.05);
          color: white;
          opacity: 1;
        }
      }
    }
  }
}
</style>