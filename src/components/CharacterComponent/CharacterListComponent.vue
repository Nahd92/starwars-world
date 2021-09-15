<template>
    <section>
        <h2>All Character</h2>
        <div class="character-container">
            <div class="character-card">
                <div class="character-img">
                    <img src="../../assets/luke.jpg" alt="luke">
                </div>
                <div class="movie-information">
                    <h3>Luke Skywalker</h3>
                    <h3>30</h3>
                </div>
                <div class="card-button">
                    <button>Reade more</button>
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
        characterImages:{},
        
    }),
    async mounted(){
        const url ="https://swapi.dev/api/people";
        try{
            const response = fetch(url);
            const data = await response.json(url);
        }
        catch(error)
        {
            console.log(error)
        }
    }
}
</script>
<style scoped>

</style>