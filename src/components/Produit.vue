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
  margin: 0; /* Remove default margin */
  max-width: 800px; /* Set a maximum width for the container */
}

.produits-list {
  list-style-type: none; /* Remove default list bullet */
  padding: 0; /* Remove default padding */
}

.produit-item {
  display: flex; /* Use flexbox for layout */
}

.produit-info {
  flex: 1; /* Take remaining space */
  display: flex; /* Use flexbox for layout */
  align-items: center; /* Center vertically */
}

.produit-image {
  margin-left: 10px; /* Add space between text and image */
}

.produit-image img {
  max-width: 100px; /* Limit image width */
  height: auto; /* Maintain aspect ratio */
  display: block; /* Ensure image is displayed as block element */
}
</style>