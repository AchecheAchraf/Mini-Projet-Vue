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
<div>
    <!-- Incrémenter la quantité d'un produit présent -->
    <form @submit.prevent="FindProduit(nomProduit,listeProduits)">
        <div>

          <label for="nomproduit" >Nom du produit :</label>
          <input type="text" id="nomproduit" v-model="nomProduit">
          <button type="submit">Trouver le produit</button>
        </div>
    </form>
          <!-- Afficher les noms des produits dans la balise select -->
          <div v-if="foundProduit">
            <h3>Produit :</h3>
            <p>ID: {{ Produit[0] }}</p>
            <p>Nom: {{ Produit[1] }}</p>
            <p>Quantité: {{ Produit[2] }}</p>
            <img :src="Produit[3]" alt="Product Image">
        </div>

        <div v-else>
            HELLO
        </div>

        
     
  </div>
</template>