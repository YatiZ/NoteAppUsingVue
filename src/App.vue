<script setup>
import {RouterView} from "vue-router"
import {ref} from "vue"


const showModal = ref(false)
const newNote = ref("")
const Notes = ref([])
const errorMessage = ref("")

function getRandomColor() {
  return 'rgb(' + 
    (Math.floor(Math.random()*56)+200) + ', ' +
    (Math.floor(Math.random()*56)+200) + ', ' +
    (Math.floor(Math.random()*56)+200) +
    ')';
}

// function getRandomColor(){
//   return "hsl(" + Math.random() * 360 + ", 100%,75%)";
// }

const addNote = () =>{
  if(newNote.value.length < 10){
    return errorMessage.value = "Note needs to be 10 characters or more"
  }
  Notes.value.push({
    id:Math.floor(Math.random() * 100000),
    text:newNote.value,
    date: new Date(),
    backgroundColor: getRandomColor()
  });
  showModal.value = false;
  newNote.value = "";
  errorMessage.value = "";
}
</script>


<template>
  
  <main>
    <!-- <RouterView/> -->
    <div v-if="showModal" class="overlay"> 
      <div class="modal">
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div> 
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button> 
      </header>
      <div class="card-container">
        <div v-for="Note in Notes" class="card" :style="{backgroundColor: Note.backgroundColor}" :key="Note.id">
         <p class="main-text">{{ Note.text }}</p>
         <p class="date">{{ Note.date.toLocaleDateString("en-US") }}</p>
        </div>
        
     </div> 
    </div>
   
  </main>
</template>

<style scoped>
main{
  height: 100vh;
  width: 100vw;

}
.container{
  max-width: 1000px;
  margin: 0 auto;
  padding: 10px;
}
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  margin-top: 20px;
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 75px;
}
header button{
  border: none;
  border-radius: 100%;
  width: 50px;
  margin-right: 80px;
  height: 50px;
  background-color: rgb(21,20,20);
  color: white;
  font-size: 20px;
  cursor: pointer;

}
.card{
  width: 235px;
  height: 235px;
  background-color: orange;
  padding: 10px;
  border-radius: 15px;
  display: flex;
  flex-direction: columns;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

.date{
 font-size: 12.5px;
 font-weight: bold;
 margin-top: 190px;
}
.card-container{
  display: flex;
  flex-wrap: wrap;

}
.overlay{
  width: 100%;
  height: 100%;
  background-color: rgba(0,0,0,0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;

}
.modal{
  width:750px ;
  background-color:white ;
  border-radius: 10px;
  position: relative;
  padding: 30px;
  display: flex;
  flex-direction: column;
  


}
.modal button{
  padding: 10px 20px;
  font-size:20px;
  color: white;
  width: 100%;
  background-color: blueviolet;
  border: none;
  cursor: pointer;
  margin-top: 15px;

}
.modal .close{
  background-color: red;
  margin-top: 7px;
}
.modal p{
  color: red;
}
</style>



