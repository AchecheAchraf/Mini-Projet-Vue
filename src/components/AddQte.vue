<script setup>
import { ref } from 'vue';
const selectedProductIdAddQte = ref(null);
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
<div class="container-addqte">
    <!-- Incrémenter la quantité d'un produit présent -->
    <h2>Incrémenter la quantité</h2>

    <form @submit="AddQte(selectedProductIdAddQte,url)">
        <div>
          <label for="nomproduit">Nom du produit :</label>
          <!-- Afficher les noms des produits dans la balise select -->
          <select v-model="selectedProductIdAddQte" id="nomproduit" class="produit-select">
            <option v-for="produit in listeProduits" :key="produit[0]" :value="produit">{{ produit[1] }}</option>
          </select>
        </div>
      <button type="submit">Incrément la quantité</button>
    </form>
  </div>
</template>

<style scoped>
.container-addqte {
  color :black;
  width: 50%; 
  margin: 0 auto; 
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.container-addqte h2 {
  text-align: center;
}

.container-addqte form {
  display: flex;
  flex-direction: column;
}

.container-addqte label {
  margin-bottom: 5px;
  width: 100px; 
}

.container-addqte select {
  padding: 8px;
  margin-bottom: 10px;
  width: calc(100% - 100px); 
}

.container-addqte div {
  display: flex;
  align-items: center;
}



.container-addqte select,
.container-addqte button {
  padding: 8px;
  margin-bottom: 10px;
}

.container-addqte button {
  background-color: #2596be;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.container-addqte button:hover {
  background-color: #0056b3;
}</style>