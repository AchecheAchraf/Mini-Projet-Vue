<script setup>
defineProps(["listeProduits","url"]);
import { ref } from 'vue';
const selectedProductIdDelete = ref(null);
function DeleteProduit(id,url) {

let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
  method: "DELETE",
  headers: myHeaders,
  };
  fetch(url+"/"+id,fetchOptions)
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

<template>
<div class="container-deleteproduit">
    <!-- Formualire pour supprimer un produit -->
    <h2>Supprimer un produit</h2>
    <form @submit="DeleteProduit(selectedProductIdDelete,url)">
        <div class="form-group">
            <label for="nomproduit">Nom du produit :</label>
            <!-- Afficher les noms des produits dans la balise select -->
            <select v-model="selectedProductIdDelete" id="nomproduit" class="produit-select">
                <option v-for="produit in listeProduits" :key="produit[0]" :value="produit[0]">{{ produit[1] }}</option>
            </select>
        </div>
        <button type="submit">Supprimer</button>
    </form>
</div>
</template>

<style scoped>
.container-deleteproduit {
  color:black;
  width: 50%; 
  margin: 0 auto; 
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.container-deleteproduit h2 {
  text-align: center;
}

.container-deleteproduit form {
  display: flex;
  flex-direction: column;
}

.container-deleteproduit label {
  margin-bottom: 5px;
  width: 100px;
}

.container-deleteproduit select {
  padding: 8px;
  margin-bottom: 10px;
  width: calc(100% - 100px); 
}

.container-deleteproduit div {
  display: flex;
  align-items: center;
}



.container-deleteproduit select,
.container-deleteproduit button {
  padding: 8px;
  margin-bottom: 10px;
}

.container-deleteproduit button {
  background-color: #2596be;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.container-deleteproduit button:hover {
  background-color: #0056b3;
}
</style>