<template>
  <div className="shop">
    <HeaderOfApp/>
    <div className="shop-content">
      <div className="list-of-pizza">
        <PizzaCard
          v-for="(pizza, index) in pizzaList"
            :key="index"
            :pizzaName="pizza.pizzaName"
            :description="pizza.description"
            :cost="pizza.cost"
            :mass="pizza.mass"
            :amount="getAmountPizzaById(index)"
            @addPizzaToCart="setPizzaInCart(index,$event.amount)"
        />
      </div>
    </div>
    <FooterOfApp/>
    <LittleCart
      :cart="cart"
      :totalItems="getTotalItems"
      @createOrder="showOrder = true"
    />
    <OrderForm 
      v-if="showOrder"
      :cart="cart"
      @closeOrderForm="showOrder = false"
      @sendOrder="sendOrder()"
    >
      <OrderList
        :pizzaList="pizzaList"
        :cart="cart"
        :totalPrice="getTotalPrice"
        @addPizzaToCart="setPizzaInCart($event.id,$event.amount)"
      />
    </OrderForm>
    <ComplitedOrderMessage 
      v-if="showSuccessOrder"
      @closeComplitedOrderMessage="closeComplitedOrderMessage()"
      />
  </div>
</template>

<script>
import HeaderOfApp from './components/HeaderOfApp.vue';
import LittleCart from './components/LittleCart.vue';
import PizzaCard from './components/PizzaCard.vue';
import OrderList from './components/OrderList.vue';
import OrderForm from './components/OrderForm.vue';
import ComplitedOrderMessage from './components/ComplitedOrderMessage.vue';
import FooterOfApp from './components/FooterOfApp.vue';
export default {
  name: 'App',
  components: {
    HeaderOfApp,
    PizzaCard,
    LittleCart,
    OrderList,
    OrderForm,
    ComplitedOrderMessage,
    FooterOfApp
},
  data(){
    return{
      pizzaList:[
        {
          pizzaName: 'Пеперони',
          description: 'Пряные колбаски пепперони с легкой перчинкой, сыр моцарелла со сливочным вкусом и нежный томатный соус.',
          cost: 300,
          mass: 500,
        },
        {
          pizzaName: 'Маргарита',
          description: 'Это классическая неаполитанская пицца: пышное тесто с хрустящей корочкой, томатное пюре, пряный базилик и тягучая моцарелла.',
          cost: 250,
          mass: 300,            
        },
        {
          pizzaName: 'Капричоза',
          description: 'Итальянская пицца, приготовленная из сыра моцарелла, запеченной ветчины, грибов, артишоков и помидоров.',
          cost: 400,
          mass: 550,            
        },
      ],
      cart:[],
      showOrder: false,
      showSuccessOrder: false,
    }
  },
  computed:{
    getTotalItems(){
      let totalItems = 0;
      this.cart.forEach((position)=>{
        totalItems += position.amount;
      })
      return totalItems;
    },
    getTotalPrice(){
      let totalPrice = 0;
      this.cart.forEach((position)=>{
        totalPrice += this.pizzaList[position.id].cost * position.amount;
      })
      return totalPrice;
    },
  },
  methods:{
    getAmountPizzaById(id){
      let searchedPosition = this.cart.find(position => position.id === id);
      if(searchedPosition){
        return this.cart[this.cart.indexOf(searchedPosition)].amount;
      } else {
        return 0;
      }
    },
    setPizzaInCart(id,amount){
      let searchedPosition = this.cart.find(position => position.id === id);
      if(searchedPosition){
        if(amount === 0){
          this.cart.splice(this.cart.indexOf(searchedPosition),1);
        } else{
          this.cart[this.cart.indexOf(searchedPosition)].amount = amount;
        }
      } else {
        this.cart.push({
          id: id,
          amount: amount,
        });
      }
    },
    sendOrder(){
      this.showOrder = false;
      this.showSuccessOrder = true;
      console.log('Данные отправлены');
    },
    closeComplitedOrderMessage(){
      this.cart = [];
      this.showSuccessOrder = false;
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
  @media (min-width: 1200px){
    .shop-content{
      width: 1100px;
    }
  }
  @media (min-width: 992px) and (max-width: 1199.99px) {
    .shop-content{
      width: 920px;
    }    
  }
  @media (min-width: 700px) and (max-width: 991.99px) {
    .shop-content{
      width: 570px;
    }    
  }  
  @media(min-width: 700px) {
    .list-of-pizza{
      justify-content: space-between;
    }
  }
  @media (max-width: 699.99px) {
    .shop-content{
      width: 280px;
    }    
    .list-of-pizza{
      justify-content: center;
    }
  } 
  *{
    margin: 0;
    font-family: Roboto;
  }
  .shop-content{
    margin: 30px auto;
    min-height: calc(100vh - 200px);
  }
  .list-of-pizza{
    display: flex;
    flex-wrap: wrap;
  }
  button{
    color: #fff;
    text-decoration: none;
    user-select: none;
    background: rgb(212,75,56); 
    padding: .7em 1.5em;
    border: 0;
  }
  button:hover{
      background: rgb(232,95,76);
      cursor: pointer;
  }
  button:active{
      background: rgb(152,15,0);
  }
</style>