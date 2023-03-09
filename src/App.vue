
<script setup>
import {ref} from 'vue'

  const showModal = ref(false)
  const newNote = ref("")
  const errMessage = ref("")
  const Notes = ref([])

  function getRandomColor() {
    return "hsl("+Math.random()*360 + ", 100%, 75%)";
  }

  const addNote = () => {
    if (newNote.value.length>9){
      Notes.value.push({
        id: Math.floor(Math.random() * 1000000),
        text: newNote.value,
        date: new Date(),
        backgroundColor: getRandomColor()
      });
      showModal.value = false
      newNote.value = ""
      errMessage.value = ""
    }else{
      return errMessage.value = "Note must be minimum 10 character!"
    }
  }

</script>


<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <textarea v-model.time="newNote" name="note" id="note" cols="30" rows="10"></textarea>
        <p v-if="errMessage">{{errMessage}}</p>
        <button @click="addNote()">Add Note</button>
        <button class="close" @click="showModal = false">Close</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div v-for="note in Notes" class="card" :style="{backgroundColor: note.backgroundColor}">
          <p class="main-text">{{note.text}}</p>
          <p class="date">{{note.date.toLocaleDateString("en-US")}}</p>
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
  padding: 10px;
  margin: 0 auto;
}

header{
  display: flex;
  justify-content: space-between;
  align-items: center;
}
h1{
  font-weight: bold;
  margin-bottom: 25px;
  font-size: 50px;
}
.container button{
   height: 50px;
   width: 50px;
   cursor: pointer;
   background-color: black;
   border-radius: 100%;
   color: white;
   font-size: 20px;
}
.card{
  width: 225px;
  height: 225px;
  background-color: rgb(220, 158, 35);
  padding: 10px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-left: 20px;
  margin-bottom: 10px;
  color: rgb(9, 9, 9);
}
.date{
  font-weight: bold;
  font-size: 10px;
  color: black;
}
.cards-container{
  display: flex;
}

.overlay{
  position: absolute;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.77);
  z-index: 10;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal{
  width: 750px;
  background-color: white;
  border-radius: 10px;
  position: relative;
  padding: 30px;
  display: flex;
  flex-direction: column;
}

.modal button{
  font-size: 20px;
  padding: 10px;
  width: 100%;
  background-color: blueviolet;
  color: white;
  cursor: pointer;
  margin-top: 10px;
  border: none;
}
.modal .close{
  background-color: red;
}
.modal p{
  color: red;
}
</style>