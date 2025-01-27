<template>
    <div 
        class="card" 
        @mouseenter="mouseHover(true)" 
        @mouseleave="mouseHover(false)"
    >
        <div class="card__img">
            <img class="image" :src="imageUrl" alt="img">
            <span class="discount-percent">{{ discountPercent }}</span>
            <component
                :is="isFavorite ? 'FavoriteIcon' : 'FavoriteActiveIcon'"
                class="is-favorite"
                @click="onClickFavorite"
            />
        </div>
        <div class="card__info">
            <div class="card__info--prices" >
                <h3  class="card__info--name">{{ name }} </h3>
                <span class="price">
                    {{ price }} руб.
                </span>
                <span class="discount">
                    {{ discount }} руб.
                </span>
            </div>
            <div class="sizes-available" v-if="expanded" :class="{active: expanded}">
                <div>
                    <p class="sizes-available__name">Размеры в наличии:</p>
                    <productSize 
                        :sizes="sizes"
                        :value="selectedSize"
                        @click="selectSize"
                    />
                </div>
                <div>
                    <button class="sizes-available__btn">КУПИТЬ</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import FavoriteActiveIcon from './icons/FavoriteActiveIcon.vue'
import FavoriteIcon from './icons/FavoriteIcon.vue'
import ProductSize from './ProductSize.vue'

export default {
    components: { ProductSize, FavoriteActiveIcon, FavoriteIcon },
    props:({
        image: {
            type: String,
            default: null
        },
        name: {
            type: String,
            default: null
        },
        discountPercent: {
            type: String,
            default: null
        },
        price: {
            type: Number,
            default: null
        },
        sizes: {
            type: Array,
            default: []
        },
        isFavorite: {
            type: Boolean,
            default: null
        },
        onClickFavorite:{
            type: Function,
            default: null
        }
    }),
    data() {
        return {
            expanded: false,
            selectedSize: null,
        }
    },
    computed: {
        imageUrl() {
            return new URL(`../assets/img/${this.image}`, import.meta.url)
        },
        discount() {
            const parcedPercent = parseInt(this.discountPercent) * -0.01 
            const discountValue = this.price * parcedPercent
            return Math.floor(this.price - discountValue)
        }
    },
    methods: {
        mouseHover(value) {
            this.expanded = value;
        },
        selectSize(value) {
            this.selectedSize = value
        },
    },
}
</script>

<style scoped>
.active{
    position:absolute;
    z-index: 1;
    background-color: #FFFFFF;
    width: 362px;
    padding: 9px 14px 19px 16px
}

/* .activeInfo{
    position:absolute;
    width: 362px;
    z-index: 1;
    background-color: #FFFFFF;
    padding-top: 13px;
    padding-left: 14px;
} */
.card {
    width: 332px;
}
.card__img {
    position: relative;
    height: 444px;
}
.card__info--name {
    color: #2D2D2D;
    font-size: 19px;
    line-height: 24px;
    padding-top: 13px;
}
.card__info--prices {
    gap: 5px;
    margin-top: 6px;
}
.discount-percent {
    top: 8px;
    left: 8px;
    width: 41px;
    height: 24px;
    position: absolute;
    color: #D01345;
    background-color: #FFFFFF;
    font-size: 12px;
    line-height: 24px;
    justify-content: center;
    display:flex;
    align-items: center;
}
.is-favorite {
    position: absolute;
    bottom: 16px;
    right: 16px;
}
.price {
    text-decoration: line-through;
    color: #2D2D2D;
    font-size: 12px;
    line-height: 24px;
    opacity: 70%;
}
.discount {
    color: #D01345;
    font-size: 16px;
    line-height: 24px;
}
.sizes-available {
    display: flex;
    justify-content: space-between;
}
.sizes-available__name {
    color:#2D2D2D;
    font-size: 14px;
    line-height: 16px;
    opacity: 60%;
    margin-bottom: 8px
}
.sizes-available__btn {
    width: 100px;
    height: 48px;
    background-color: #2D2D2D;
    color: #FFFFFF;
    font-size: 12px;
    line-height: 24px;
    cursor: pointer;
}
</style>

