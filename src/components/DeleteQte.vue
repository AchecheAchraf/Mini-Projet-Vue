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
  else{
    alert("Impossible de décrimenter la quantité du ce produit")
  }
}

</script>

<template>
<div class="container-deleteqte">
    <!-- Décrimenter la quantité d'un produit présent -->
    <h2>Décrimenter la quantité</h2>
    <form @submit="DeleteQte(selectedProductId,url)">
        <div>
          <label for="nomproduit">Nom du produit :</label>
          <select v-model="selectedProductId" id="nomproduit" class="produit-select">
            <option v-for="produit in listeProduits" :key="produit[0]" :value="produit">{{ produit[1] }}</option>
          </select>
        </div>
      <button type="submit">Décrimenter la quantité</button>
    </form>
  </div>
</template>

<style>
.container-deleteqte {
  width: 50%; 
  margin: 0 auto; 
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.container-deleteqte h2 {
  text-align: center;
}

.container-deleteqte form {
  display: flex;
  flex-direction: column;
}

.container-deleteqte label {
  margin-bottom: 5px;
  width: 100px; 
}

.container-deleteqte select {
  padding: 8px;
  margin-bottom: 10px;
  width: calc(100% - 100px); 
}

.container-deleteqte div {
  display: flex;
  align-items: center;
}



.container-deleteqte select,
.container-deleteqte button {
  padding: 8px;
  margin-bottom: 10px;
}

.container-deleteqte button {
  background-color: #9AC8EB;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.container-deleteqte button:hover {
  background-color: #0056b3;
}</style>