<script setup>
defineProps(["listeProduits","url"]);



//Fonction pour décrémentation la quantité
function DeleteQte(produit,url) {
let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({id: produit[0],nom : produit[1], qte: produit[2] - 1 ,photo: produit[3]}), 
  };
  console.log(produit[2])
  if (produit[2]>1){
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
    });}
    //Avec cette fonction on n'a pas le droit pour mettre la quantité < ou = à 0 sinon on a besoin de supprimer le produit
  else{
    alert("Impossible de décrimenter la quantité du ce produit")
  }
}

</script>

<template>
<div>
    <!-- Décrimenter la quantité d'un produit présent -->
    <form @submit="DeleteQte(selectedProductId,url)">
        <div>
          <label for="nomproduit">Nom du produit :</label>
          <select v-model="selectedProductId" id="nomproduit" class="produit-select">
            <option v-for="produit in listeProduits" :key="produit[0]" :value="produit">{{ produit[1] }}</option>
          </select>
        </div>
      <button type="submit">Supprimer du quantité</button>
    </form>
  </div>
</template>