<template>
    <div 
        class="card" 
        @mouseenter="mouseHover(true)" 
        @mouseleave="mouseHover(false)"
    >
        <div class="card__img">
            <img class="image" :src="imageUrl" alt="img">
            <span class="discount-percent">{{ discountPercent }}</span>
            <FavoriteIcon
                class="is-favorite"
                :class="{'is-favorite--active': isFavorite}"
                @click="favoriteHandler"
            />
        </div>
        <div class="card__info" :class="{active: expanded}">
            <div class="card__info--prices" >
                <h3 class="card__info--name">{{ name }}</h3>
                <span class="price">
                    {{ price }} руб.
                </span>
                <span class="discount">
                    {{ discount }} руб.
                </span>
            </div>
            <div class="sizes-available" v-if="expanded">
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
import FavoriteIcon from './icons/FavoriteIcon.vue'
import ProductSize from './ProductSize.vue'

export default {
    components: { ProductSize, FavoriteIcon },
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
    }),
    emits: ['click:favorite'],
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
        favoriteHandler() {
            this.$emit('click:favorite')
        }
    },
}
</script>

<style scoped>
.active{
    --px: 14px;
    position: absolute;
    z-index: 1;
    left: calc(var(--px) * -1);
    background-color: var(--white);
    width: calc(var(--width) + calc(var(--px) * 3));
    padding: 0 var(--px) 19px;
}
.card {
    --width: 332px;
    width: var(--width);
    position: relative;
}
.card__img {
    position: relative;
    height: 444px;
}
.card__info--name {
    color: var(--gray);
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
    color: var(--red);
    background-color: var(--white);
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
    cursor: pointer;
    fill: none !important;
}
:global(.is-favorite .path-1) {
    fill: var(--white);
} 
:global(.is-favorite .path-2) {
    fill: var(--gray);
} 
:global(.is-favorite--active .path-1) {
    fill: var(--red);
} 
:global(.is-favorite--active .path-2) {
    fill:  var(--white);
} 

.price {
    text-decoration: line-through;
    color: var(--gray);
    font-size: 12px;
    line-height: 24px;
    opacity: 70%;
}
.discount {
    color: var(--red);
    font-size: 16px;
    line-height: 24px;
}
.sizes-available {
    display: flex;
    justify-content: space-between;
    padding-top: 9px;
}
.sizes-available__name {
    color: var(--gray);
    font-size: 14px;
    line-height: 16px;
    opacity: 60%;
    margin-bottom: 8px
}
.sizes-available__btn {
    width: 100px;
    height: 48px;
    background-color: var(--gray);
    color: var(--white);
    font-size: 12px;
    line-height: 24px;
    cursor: pointer;
}
</style>

