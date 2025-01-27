<template>
    <div class="product-size">
        <button 
            v-for="size in sizes" 
            :key="size"
            class="product-size__btn" 
            :class="{'product-size__btn--active': value === size }"
            @click="clickHanlder(size)"
        >
            {{ size }}
        </button>
    </div> 
</template>

<script>
export default {
    props: {
        sizes: {
            type: Array,
            default: []
        },
        value: {
            type: [String, Number],
            default: null,
        }
    },
    emits: ['click'],
    methods:{
      clickHanlder(value) {
        this.$emit('click', value)
      }      
    }
}
</script>

<style scoped>
.product-size {
    display:flex;
    flex-direction: row;
    gap: 16px;
}

.product-size__btn {
    font-size: 14px;
    line-height: 20px;
    background-color: #FFF;
    cursor: pointer;
    user-select: none;
}

.product-size__btn--active {
    color: red;
}

</style>


