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
        console.log(response.json)
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
 <div>
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