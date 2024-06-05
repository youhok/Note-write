<template>
  <div>
    <header>
      <div class="container text-center mt-5 p-5">
        <div class="row">
          <div class="col-6">
            <h1>My Note</h1>
          </div>
          <div class="col-6">
            <button class="tagglo" data-bs-target="#exampleModalToggle" data-bs-toggle="modal">
              <i class="bi bi-plus-lg"></i>
            </button>
          </div>
        </div>
      </div>
    </header>
    <section>
      <div class="container">
        <div class="row">
          <div class="col-12"></div>
          <div class="card-container">
            <div
              v-for="note in notestore"
              :key="note.id"
              class="card"
              :style="{ backgroundColor: note.backgroundColor }"
            >
              <p class="main-text">{{ note.text }}</p>
              <p class="date">{{ note.date.toLocaleDateString('en-US') }}</p>
            </div>
          </div>
        </div>
      </div>
    </section>
    <!-- modal -->
    <div
      class="modal fade"
      id="exampleModalToggle"
      aria-hidden="true"
      aria-labelledby="exampleModalToggleLabel"
      tabindex="-1"
    >
      <div class="modal-dialog modal-dialog-centered">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="exampleModalToggleLabel">Note</h1>
          </div>
          <div class="modal-body">
            <textarea
              class="note"
              name="note"
              id="note"
              cols="30"
              rows="10"
              v-model="newnote"
            ></textarea>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-danger" data-bs-dismiss="modal" aria-label="Close">
              Close
            </button>
            <button
              class="btn Addbutton"
              data-bs-target="#exampleModalToggle2"
              data-bs-toggle="modal"
              @click="addNote"
            >
              Add Note
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newnote = ref('');

const notestore = ref([]);

function randomColor() {
  return 'hsl(' + Math.random() * 360 + ' , 100% , 75%)'
}

const addNote = () => {
  notestore.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: newnote.value,
    date: new Date(),
    backgroundColor: randomColor()
  })

  newnote.value = '';
}
</script>

<style scoped>
.note {
  width: 100%;
}
.card-container {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
}
.Addbutton {
  background-color: #e9ff70;
}

.tagglo {
  width: 60px;
  height: 60px;
  bottom: 40px;
  right: 40px;
  background-color: black;
  color: white;
  border-radius: 50px;
  text-align: center;
  font-size: 30px;
  box-shadow: 2px 2px 3px #999;
  z-index: 100;
  border: #004dff;
  transition: 0.5s;
}

.tagglo:hover {
  transform: scale(1.1);
}

.tagglo:active {
  background-color: #020cd1;
}

.arrow-up {
  width: 0;
  height: 0;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  margin-left: auto;
  margin-right: auto;
  margin-top: 35%;
  margin-bottom: 60%;
  border-bottom: 15px solid white;
}
.card {
  width: 225px;
  height: 225px;
  background-color: rgb(237, 182, 44);
  border-radius: 15px;
  display: flex;
  padding: 20px;
  flex-direction: column;
  justify-content: space-between;
  margin-right: 20px;
  margin-bottom: 20px;
}

</style>
