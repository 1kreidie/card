<template>
  <section>
    <Card 
      v-for="(item, i) in data" 
      :key="i"
      :image="item.image"
      :name="item.name"
      :discount-percent="item.discountPercent"
      :price="item.price"
      :sizes="item.sizes"
      :isFavorite="item.isFavorite"
    />
  </section>
</template>

<script>
import Card from "./components/Card.vue";

export default {
  components: {
    Card,
  },
  data: () => ({
    data: [
      {
        image: 'img1.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      }
    ]
  })
}
</script>
