<template>
  <section class="section">
    <Card 
      v-for="(item, i) in data" 
      :key="i"
      :image="item.image"
      :name="item.name"
      :discount-percent="item.discountPercent"
      :price="item.price"
      :sizes="item.sizes"
      :is-favorite="item.isFavorite"
      @click:favorite="setFavorite(i)"
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
      },
      {
        image: 'img2.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-20%',
        price: 3999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img3.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img4.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img5.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img6.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img7.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
      {
        image: 'img8.webp',
        name: 'Вельветовый пуховик',
        discountPercent: '-25%',
        price: 7999,
        sizes: ['S', 'M', 'L', 'XL', 'XXl'],
        isFavorite: false
      },
    ]
  }),
  methods: {
    setFavorite(i) {
      this.data[i].isFavorite = !this.data[i].isFavorite; 
    },
  },
}
</script>

<style scoped>
.section{
  margin: 100px 290px 137px 290px;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
