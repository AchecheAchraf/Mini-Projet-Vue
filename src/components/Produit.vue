<script setup>
defineProps(["listeProduits"]);
</script>
<template>
    <div class="container">
          <!-- Afficher les produits -->
        <h1>Liste des produits</h1>
        <ul class="produits-list">
        <li v-for="produit in listeProduits" :key="produit[0]" class="produit-item">
            <div class="produit-info">
                <span>{{ produit[1] }}</span> - <span>{{ produit[2] }}</span>
            </div>
            <div class="produit-image">
                <img :src="produit[3]" />
            </div>
        </li>
        </ul>
    </div>
</template>

<style>
.container {
  margin: 0; 
  max-width: 800px;
}

.produits-list {
  list-style-type: none;
  padding: 0;
}

.produit-item {
  display: flex; 
}

.produit-info {
  flex: 1; 
  display: flex;
  align-items: center; 
}

.produit-image {
  margin-left: 10px;
}

.produit-image img {
  max-width: 100px;
  height: auto;
  display: block; 
}
</style>