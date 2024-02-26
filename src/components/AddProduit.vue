<script setup>
import { ref } from 'vue';

const nomProduit = ref('');
const quantite = ref(0);
const image = ref('');
defineProps(["url"]);

//Fonction pour ajouter un produit
function AddProduit(nomProduit,quantite,image,url){
    let myHeaders = new Headers();
    myHeaders.append("Content-Type", "application/json");
    const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify({ nom : nomProduit , qte : quantite , photo : image }),
    };
    fetch(url,fetchOptions)
    .then((response) => {
        console.log(nomProduit,qte,photo)
      return response.json(); 
    })
    .then((dataJSON) => {
      console.log(dataJSON)
    })
    .catch((error) => {
      console.log(error);
    });
}
</script>
<template >
 <div class="container-addproduit">
  <h2>Ajouter un produit</h2>
  <!-- Ajoute d'un produit avec une formulaire-->
  <form @submit="AddProduit(nomProduit, quantite, image,url)">
    <div>
      <label for="nomproduit">Nom du produit:</label>
      <input type="text" id="nomproduit" v-model="nomProduit" required>
    </div>
    <div>
      <label for="quantite">Quantité:</label>
      <input type="number" id="quantite" v-model.number="quantite" required>
    </div>
    <div>
      <label for="photo">Photo :</label>
      <input type="text" id="photo" v-model="image">
    </div>
    <button type="submit">Envoyer</button>
  </form>
</div>
</template>

<style scoped>
.container-addproduit {
  color : black;
  width: 50%; 
  margin: 0 auto; 
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.container-addproduit h2 {
  text-align: center;
}

.container-addproduit form {
  display: flex;
  flex-direction: column;
}

.container-addproduit label {
  margin-bottom: 5px;
  width: 100px; 
}

.container-addproduit input {
  padding: 8px;
  margin-bottom: 10px;
  width: calc(100% - 100px);
}

.container-addproduit div {
  display: flex;
  align-items: center;
}

.container-addproduit input,
.container-addproduit button {
  padding: 8px;
  margin-bottom: 10px;
}

.container-addproduit button {
  background-color: #2596be;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.container-addproduit button:hover {
  background-color: #0056b3;
}
</style>