<template>
    <div class="order-list">
        <div 
            v-if="cart.length > 0"
            className="order-list-positions"
        >
            <p className="order-list-positions__title"> Ваш заказ:</p>
            <ul className="order-list-positions__list">
                <li
                    className="order-list-positions__position"
                    v-for="(position, index) in cart"
                    :key="index"
                >
                    <span className="order-list-positions__position-name">{{ pizzaList[position.id].pizzaName }}:</span>
                    <div  className="order-list-positions__position-amount">
                        <button
                            className="order-list-positions__position-button"
                            @click="decrementPizza(cart[index].id, position.amount)"
                        >-</button>
                        <span className="order-list-positions__position-amount-value">{{ position.amount }}</span>
                        <button
                            className="order-list-positions__position-button"
                            @click="incrementPizza(cart[index].id, position.amount)"
                        >+</button>
                        <button
                            className="order-list-positions__position-button delete"
                            @click="this.$emit('addPizzaToCart', {id: cart[index].id, amount: 0})"
                        >
                            <img src="../assets/delete-icon.svg" alt="⌫" height="14"/>
                        </button>
                    </div>
                    
                </li>
            </ul>
            <p>Итого: {{ totalPrice }} ₽</p> 
        </div>
        <div 
            v-else
            class="order-list__is-empty"
        >
            <p class="order-list__is-empty-text"> Вы не можете оформить заказ. Ваша корзина пуста</p>
        </div>
    </div>
</template>
<script>
export default {
    name: 'OrderList',
    props: {
        pizzaList: Array,
        cart : Array,
        totalPrice : Number,
    },
    methods: {
        incrementPizza(id, amount){
            if(amount < 10){
                this.$emit('addPizzaToCart', {id: id, amount: amount + 1});
            }
        },
        decrementPizza(id, amount){
            if(amount >     0){
                this.$emit('addPizzaToCart', {id: id, amount: amount - 1});
            }
        }
    }
}
</script>

<style>
@media (min-width: 760px){
.order-list-positions__list{
    height: 50vh;
    overflow: auto;
}
}

ul {
    list-style-type:  none;
    padding: 0;
}
.order-list-positions{ 
    width: 400px;
    text-align: left;
}
.order-list-positions__title{
    font-weight: 700;
    font-size: 24px;
    margin-bottom: 20px;
    /* text-align: left; */
}
.order-list-positions__position-button{
    width: 40px;
    height: 40px;
    padding: 0;
    display:inline-block;
}
.order-list-positions__position{
    display: flex;
    justify-content: space-between;
    margin-bottom: 10px;
}
.order-list-positions__position-amount-value{
    margin:0 15px;
}
.delete{
    margin-left:15px;
}
.order-list__is-empty-text{
    width: 70%;
    font-size: 32px;
    margin: 0 auto 30px;
}
</style>