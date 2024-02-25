<script setup>
import Produit from './components/Produit.vue';
import AddProduit from './components/AddProduit.vue'
import DeleteProduit from './components/DeleteProduit.vue'
import AddQte from './components/AddQte.vue'
import DeleteQte from './components/DeleteQte.vue'
import FindProduit from './components/FindProduit.vue'

import { onMounted,onUpdated,reactive } from "vue";
const listeProduits = reactive([]);
const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/16/produits";

function getProduits(){
    fetch(url)
    .then((response) => {
      return response.json();
    })
    .then((dataJSON) => {
      let produits = dataJSON
      listeProduits.splice(0,listeProduits.length);
      for (let prod of produits){
        listeProduits.push([prod.id,prod.nom,prod.qte,prod.photo])
      }
    })
    .catch((error) => {
      console.log(error);
    });    
}
onMounted(() => {getProduits()})
onUpdated(() => {getProduits()})
</script>

<template>

  <div>
    <FindProduit :listeProduits="listeProduits"/>
    <Produit :listeProduits="listeProduits" :url="url"/>
    <AddProduit :url="url"/>
    <DeleteProduit :listeProduits="listeProduits" :url="url"/>
    <AddQte :listeProduits="listeProduits" :url="url"/>
    <DeleteQte :listeProduits="listeProduits" :url="url"/>
  </div>
</template>

<style>
/* Reset margin and padding */
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
