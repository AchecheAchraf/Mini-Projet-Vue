<script setup>

import { ref } from 'vue';
defineProps(["listeProduits"]);

const nomProduit = ref('');
const Produit =ref([]);
const foundProduit=ref(false)



function FindProduit(nomprod,listeProduits){
    for (let prod of listeProduits){
        if (prod[1].toUpperCase() === nomprod.toUpperCase()){
            console.log(prod[1])
            Produit.value=prod
            console.log(Produit)
            foundProduit.value=true
            break
        }
        else{
            Produit.value=[]
            foundProduit.value=false
            }
    }
}

</script>

<template>
  
    <div class="navbar">
      <form @submit.prevent="FindProduit(nomProduit,listeProduits)">
          <div class="text-navbar"><h1>Frigo</h1></div>
            <div class="search-container">
              <input type="text" id="nomproduit"  placeholder="Produit" v-model="nomProduit">
              <button type="submit">Rechercher</button>
            </div>
    </form>
  </div>
<div>
          <!-- Afficher les noms des produits dans la balise select -->
          <div v-if="foundProduit" class="found-produit">
            <h3>Produit :</h3>
            <p>ID: {{ Produit[0] }}</p>
            <p>Nom: {{ Produit[1] }}</p>
            <p>Quantité: {{ Produit[2] }}</p>
            <img :src="Produit[3]" alt="Product Image">
        </div>

  </div>
</template>

<style>
.found-produit {
  margin-top: 51px;
}
body {
  margin: 0;
  padding: 0;
}

.navbar {
  background-color: #007bff;
  height: 70px;
  width: 100%;
  position: fixed;
  top: 0;
  left:0;
  right:0;
  z-index: 1000;
}

.text-navbar {
  color: #FFFFFF;
  float: left;
  margin-top: -2px;
  margin-left: 20px;
}

.search-container {
  float: right;
  margin-top: 15px;
  margin-right: 20px;
}

.search-container input {
  margin: 5px;
  padding: 10px;
  border: none;
  font-size: 17px;
}

.search-container button {
  margin: 5px;
  padding: 10px 20px;
  background: #8AAFAE;
  color: white;
  border: none;
  cursor: pointer;
}

</style>