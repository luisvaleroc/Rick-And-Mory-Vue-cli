
<template>
  <div id="app">
        <div>
            {{errors.error}}
        </div>
        <div v-for="item in personajes" :key="item.id">
         
             <input type="text" v-model="item.name" @change="editar()">
             {{item.name}}
         <img :src="item.image" alt=""/><br>
         <button @click="borrar(item.name)">lol</button>
         <input type="editar">
         
        </div>
       
    </div>
</template>




<script>
import axios from "axios";

export default {
    data() {
        return {
            personajes: [],
            errors : []
            }
    },

    methods: {
          mostrar(){
     
          axios.get('https://rickandmortyapi.com/api/character')
            .then(response => { 
                let respuestaApi = response.data.results;
                this.personajes = respuestaApi;
             //   console.log(this.personajes);  
            })
            .catch(e => {
               
                this.errors = e.response.data;
                console.log( this.errors)
            } );

        },

        borrar(name) {
            console.log(name);
           const index = this.personajes.findIndex(item => item.name === name)
           this.personajes.splice(index,1)
         //  const lol =  this.personajes.slice(0,index).concat(this.personajes.slice(index+1))
         // let personajes =  this.personajes;

         
  //   const immutableDelete = (personajes, index)  => {
  // return personajes.slice(index,1).concat(personajes.slice(index+1))
//}
           console.log(this.personajes);
          // console.log(lol);
        //   console.log({inmu: immutableDelete()});
        
        },
        editar(){
         //  const index = this.personajes.findIndex(item => item.id === id)
          // this.personajes[index].name = name; 
           console.log( this.personajes);
        }
    },
    created () {
        this.mostrar();  
        
      }
}

</script>