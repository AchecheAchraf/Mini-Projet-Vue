<script setup>
defineProps(["listeProduits","url"]);

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
<div>
    <!-- Formualire pour supprimer un produit -->
    <form @submit="DeleteProduit(selectedProductId,url)">
        <div>
          <label for="nomproduit">Nom du produit :</label>
          <!-- Afficher les noms des produits dans la balise select -->
          <select v-model="selectedProductId" id="nomproduit" class="produit-select">
            <option v-for="produit in listeProduits" :key="produit[0]" :value="produit[0]">{{ produit[1] }}</option>
          </select>
        </div>
      <button type="submit">Supprimer</button>
    </form>
  </div>
</template>