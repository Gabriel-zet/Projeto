<template>
  <div class="main">
    <h1>Create Categories</h1>
    <label for="title">Title</label>
    <input
      type="text"
      class="input is-link"
      placeholder="Titulo"
      name="title"
      id="title"
      v-model="title"
    />
    <label for="Description">Description</label>
    <input
      type="text"
      class="input is-link"
      placeholder="Descrição"
      name="Description"
      id="Description"
      v-model="desc"
    />
    <button @click="createCategory" class="button is-success">Criar</button>
    <div v-if="showPopup" id="popup" class="popup">
      <div class="popup-content">
        <span class="close" @click="closePopup">&times;</span>
        <p>Criado com sucesso!</p>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "",
      desc: "",
      showPopup: false,
    };
  },
  methods: {
    createCategory() {
      axios
        .post(`http://localhost:3330/Category`, {
          title: this.title,
          description: this.desc,
        })
        .then((response) => {
          console.log("Criado com sucesso!", response);
          this.showPopup = true;
        })
        .catch((err) => {
          console.warn("Ocorreu um error", err);
        });
    },
    closePopup() {
      this.showPopup = false;
    },
  },
};
</script>

<style>
body {
  font-family: Arial, sans-serif;
}

#myButton {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}

.popup {
  display: block; /* Mantenha o display como block e controle a visibilidade com v-if */
  position: fixed;
  z-index: 1;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  overflow: auto;
  background-color: rgba(0, 0, 0, 0.4);
}

.popup-content {
  background-color: #fefefe;
  margin: 15% auto;
  padding: 20px;
  border: 1px solid #888;
  width: 80%;
  max-width: 300px;
  text-align: center;
}

.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>