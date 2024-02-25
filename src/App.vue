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

//Fonction pour afficher tous les produits
function getProduits(){
    fetch(url)
    .then((response) => {
        console.log(response.json)
      return response.json();
    })
    .then((dataJSON) => {
      console.log(dataJSON)
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
  <Produit :listeProduits="listeProduits" :url="url"/>
  <AddProduit :url="url"/>
  <DeleteProduit :listeProduits="listeProduits" :url="url"/>
  <AddQte :listeProduits="listeProduits" :url="url"/>
  <DeleteQte :listeProduits="listeProduits" :url="url"/>
  <FindProduit :listeProduits="listeProduits"/>
  <!--
  
  
  
  
  
  -->
  
 
</template>