<template>
    <div className="cart">
        <div 
            v-if="totalItems>0"
            className="cart-list"
        >
            <p className="cart-list__total-pizza-label">Пицц в корзине:  </p>
            <p className="cart-list__total-pizza-value">{{ totalItems }}</p>
            <button 
                className="cart-list__order-button"
                @click="this.$emit('createOrder')"
            > Оформить заказ </button>
        </div>
        <div 
            v-else
            className="cart__empty-card"
        >
            <p className="cart__empty-card-message">
                Ваша корзина пустая
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CartOfShop',
    props: {
        cart: Array,
        totalItems: Number,
    },
}
</script>

<style>
@media (min-width: 500px) {
    .cart{
        width: 260px;
    }    
}
@media (max-width: 499.99px) {
    .cart{
        width: 100vw;
    }    
} 
.cart{
    background-color: white;
    border-left:  3px solid rgb(212,75,56);
    border-top:  3px solid rgb(212,75,56);
    border-radius: 5px 0 0 0;

    height: 100px;

    text-align: center;
    display	: table;

    position: fixed;
    bottom: 0;
    right: 0;
}
.cart-list, .cart__empty-card{
    display	: table-cell;
	vertical-align : middle;
}
.cart-list__total-pizza-value{
    font-weight: 700;
}
</style>