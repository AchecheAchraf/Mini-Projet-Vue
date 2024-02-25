<script setup>
import Produit from './components/Produit.vue';
import AddProduit from './components/AddProduit.vue'
import DeleteProduit from './components/DeleteProduit.vue'
import AddQte from './components/AddQte.vue'
import DeleteQte from './components/DeleteQte.vue'
import FindProduit from './components/FindProduit.vue'

import { onMounted,onUpdated,reactive } from "vue";
const listeProduits = reactive([]);
const url = "https://webmmi.iut-tlse3.fr/~pecatte/frigo/public/2/produits";

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
<div class="page">
  <div class="nav">
    <FindProduit :listeProduits="listeProduits"/>
  </div>
  <div class="container">
    <div class="left">
      <Produit :listeProduits="listeProduits" :url="url"/>
    </div>
    <div class="right">
      <AddProduit :url="url"/>
      <DeleteProduit :listeProduits="listeProduits" :url="url"/>
      <AddQte :listeProduits="listeProduits" :url="url"/>
      <DeleteQte :listeProduits="listeProduits" :url="url"/>
    </div>
  </div>
</div>
</template>

<style>
.page {
  background-color: #B6D8F2;
  display: flex;
  flex-direction: column;
  height: 100vh; 
}

.container {
  margin-top: 40px;
  flex: 1; 
  display: flex;
  color:white;
  justify-content: center; 
}

.left, .right {
  flex: 1; 
}

.left {
  background-color: #B6D8F2;
}

.right {
  background-color: #B6D8F2;
 
}

</style>
