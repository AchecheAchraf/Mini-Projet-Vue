<script setup>

import { ref ,onMounted, reactive} from 'vue';
defineProps(["listeProduits","url"]);

function AddQte(produit,url) {
let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({id: produit[0],nom : produit[1], qte: produit[2] + 1 ,photo: produit[3]}), // Utilisation de l'opérateur d'incrémentation qte++

  };
  fetch(url,fetchOptions)
  .then((response) => {
      console.log(response.json)
      console.log(produit[2])
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

<template>
<div>
    <!-- Incrémenter la quantité d'un produit présent -->
    <form @submit="AddQte(selectedProductId,url)">
        <div>
          <label for="nomproduit">Nom du produit :</label>
          <!-- Afficher les noms des produits dans la balise select -->
          <select v-model="selectedProductId" id="nomproduit" class="produit-select">
            <option v-for="produit in listeProduits" :key="produit[0]" :value="produit">{{ produit[1] }}</option>
          </select>
        </div>
      <button type="submit">Ajouter du quantité</button>
    </form>
  </div>
</template>