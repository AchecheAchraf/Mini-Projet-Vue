<script setup>
defineProps(["listeProduits"]);
</script>
<template>
  <div class="produits">
      <h2>Liste des produits</h2>
      <ul class="produits-list">
          <li v-for="produit in listeProduits" :key="produit[0]" class="produit-item">
              <div class="produit-info">
                  <span>Nom : {{ produit[1] }}</span> - <span>Quantité : {{ produit[2] }}</span>
              </div>
              <div class="produit-image">
                  <img :src="produit[3]" />
              </div>
          </li>
      </ul>
  </div>
</template>

<style>
.produit-item {
  background-color: #9AC8EB;
  border-radius: 10px;
  margin-bottom: 10px; 
  padding: 10px; 
}

.produit-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.produit-info {
  color: white;
}

.produit-image img {
  max-width: 100px; 
  border-radius: 5px;
}

.produits {
  margin-top:37px;
  text-align: center; 
}

.produits-list {
  list-style-type: none;
  padding: 0;
}

.produit-item {
  display: flex; 
  align-items: center; 
  justify-content: center;
  margin: 10px; 
}

.produit-info {
  margin-right: 10px; 
}

.produit-image img {
  width: 100px; 
}
</style>