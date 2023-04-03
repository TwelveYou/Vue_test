<template>
    <div className="pizza-card">
        <h3 className="pizza-card__name">{{ pizzaName }}</h3>
        <img 
            className="pizza-card__image"
            :src='image' 
            :alt='pizzaName'
            width="200"
            height="150"
        >
        <p className="pizza-card__description">{{ description }}</p>
        <div className="pizza-card__cost-and-mass">
            <p>{{ cost }} ₽</p>
            <p>{{ mass }} гр.</p>
        </div>
        <div 
            className="pizza-card-amount"
            v-if="amount"
        >
            <button 
                className="pizza-card-amount__button-operation"
                v-on:click="decrementPizza"
            >-</button>
            <span className="pizza-card-amount__value">{{ amount }}</span>
            <button 
                className="pizza-card-amount__button-operation"
                v-on:click="incrementPizza"
            >+</button>
        </div>
        <button 
            className="pizza-card__button-add"
            @click="addToCart"
            v-else
        > В корзину </button>
    </div>
</template>

<script>
    import image from '../assets/pizzaPlug.png';
    export default{
        name: 'PizzaCard',
        props: {
            pizzaName : String,
            description : String,
            cost : Number,
            mass : Number,
            amount : Number,
        },
        data() {
            return{
                image: image,
            }
        },
        methods: {
            addToCart(){
                this.$emit('addPizzaToCart', {amount: 1});
            },
            incrementPizza(){
                if(this.amount + 1 <= 10){
                    this.$emit('addPizzaToCart', {amount: this.amount + 1});
                }
            },
            decrementPizza(){
                if(this.amount - 1 >= 0){
                    this.$emit('addPizzaToCart', {amount: this.amount - 1});
                }
            },
        }
    }   
</script>

<style>
    .pizza-card{
        width: 250px;
        box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
        height: 410px;
        text-align: center;
        margin-bottom: 30px;
        position: relative;
    }
    .pizza-card__name, .pizza-card__image, .pizza-card__description{
        padding-top: 13px;
    }
    .pizza-card__name{
        font-size: 22px;
    }
    .pizza-card__button-add{
        margin-top: 13px;
    }
    .pizza-card__description{
        text-align: left;
        padding-left: 25px;
        padding-right: 25px;
        font-size: 14px;
        height: 97px;
    }
    .pizza-card__cost-and-mass{
        padding: 13px 25px 0;
        display: flex;
        justify-content: space-between;
    }
    .pizza-card-amount__button-operation{
        color: #fff; 
        text-decoration: none; 
        user-select: none;
        background: rgb(212,75,56);
        padding: .7em 1em;
        border: 0;
    }
    .pizza-card-amount__value{
        padding: 0 1em;
    }
    .pizza-card__button-add, .pizza-card-amount{
        position: absolute;
        bottom: 15px;
        display: block;
        left: 50%;
        transform: translate(-50%, 0);
    }

</style>