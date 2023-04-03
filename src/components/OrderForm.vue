<template>
    <div className="order">
        <div className="order__blackout"></div>
        <div className="order__wrap-table">
            <div className="order__wrap-flex">
                <form v-if="cart.length" className="order__form">
                    <div className="order-input">
                        <label className="order-input__label" for="input-full-name">ФИО</label>
                        <input className="order-input__field" type="text" id="input-full-name" v-model="fullName">
                    </div>
                    <div className="order-input">
                        <label className="order-input__label" for="input-phone">Телефон</label>
                        <input className="order-input__field" type="text" id="input-phone" v-model="phoneNumber">
                    </div>
                    <div className="order-input">
                        <label className="order-input__label" for="input-full-address">Адрес</label>
                        <textarea className="order-input__field" id="input-address" v-model="address"></textarea>
                        <!-- <input className="order-input__field" type="text" id="input-address" v-model="address"> -->
                    </div>
                    <!-- <button @click="sendOrderOnServer">Отправить заказ</button> -->
                </form>
                <slot></slot>
            </div>
            <div className="order-buttons" v-if="cart.length">
                <div className="order-buttons_wrapper-length">
                    <button 
                        className="order-buttons__button"
                        @click="this.$emit('sendOrder')"
                    >Отправить заказ</button>
                    <button @click="this.$emit('closeOrderForm')">Отмена</button>
                </div>
                <button className="order-buttons__button-close" @click="this.$emit('closeOrderForm')">×</button>
            </div >
            <button 
                v-else
                className="order-buttons__button-return"
                @click="this.$emit('closeOrderForm')"
            >Вернуться к каталогу</button>
        </div>
    </div>
</template>
<script>
export default {
    name: 'OrderForm',
    props:{
        cart: Array,
    },
    data() {
        return {
            fullName: '',
            phoneNumber: '',
            address: '',
        }
    },
    methods:{
        sendOrderOnServer(){
            console.log(`Инфо о заказчике: ${this.fullName} (${this.phoneNumber}). \nАдрес: ${this.address}`);
        }
    }
}
</script>
<style>
@media (min-width: 1200px){
    .order__form{
        width: 350px;
        margin-right: 50px;
    }
    .order-list-positions{
        width: 400px;        
    }
    .order-buttons_wrapper-length{
        width: 350px;
    }
    .order-input__field{
        width: 340px;
    }
    .order-buttons{
        width: 800px;
    }
}
@media (min-width: 760px) and (max-width: 1199.99px) {
    .order__form{
        width: 300px;
        margin-right: 40px;
    }
    .order-list-positions{
        width: 300px;        
    }
    .order-buttons_wrapper-length{
        width: 300px;
    }
    .order-input__field{
        width: 298px;
    }
    .order-buttons{
        width: 640px;
    }
}
@media (min-width: 760px){
    .order__wrap-flex{
        display:flex;
        flex-wrap: wrap;
        justify-content: center;
    }
    .order__wrap-table{
        display	: table-cell;
        vertical-align : middle;
    }
    .order-buttons__button-close{
        top: 50px;
        right: 50px;
        font-size: 50px;
        width: 70px;
        height: 70px;
        background: none;
    }
    .order-buttons {
        margin-top: -30px;
    }
}

@media (max-width: 759.99px) {
    .order__form{
        width: 280px;
        margin-right: 0;
    }
    .order-list-positions{
        width: 280px;        
    }
    .order-buttons_wrapper-length{
        width: 280px;
    }
    .order-input__field{
        width: 274px;
    }
    .order-buttons{
        width: 280px;
    }
    .order__wrap-flex {
        display: block;    
        margin: auto;
        width: 280px;
    }
    .order__wrap-table{
        height: calc(100vh - 70px);
        overflow: auto;
        padding-top: 70px;
    }
    .order-buttons__button-close{
        top: 15px;
        right: 15px;
        width: 55px;
        height: 55px;
        background-color: rgba(0,0,0,0.8);
        font-size: 45px;
        border-radius: 35px;
    }
    .order-buttons__button-close:hover{
        color: rgba(0,0,0,0.8);
    }
    .order-buttons{
        padding-bottom: 20px;
        margin-top: 20px;
    }
} 
.order{
    position: fixed;
    top: 0;
    left: 0;

    min-height: 100vh;
    width: 100vw;

    background-color: rgba(0, 0, 0, 0.9);
    color: white;
    text-align: center;

    display	: table;
}
.order__form{
    /* width: 350px; */
    margin-right: 50px;
}
/* .order__wrap-table{
    display	: table-cell;
    vertical-align : middle;
} */
/* .order__wrap-flex{
    display:flex;
    flex-wrap: wrap;
    justify-content: center;
} */

.order-input{
    text-align: left;
}
.order-input__label{
    display: block;
}
/* .order-input__field{
    width: 340px;
} */
.order-buttons{
    /* width: 750px; */
    margin-right: auto;
    margin-left: auto;
    text-align: left;
}
/* .order-buttons__button{
    margin-right: 200px;
} */
.order-buttons_wrapper-length{
    /* width: 350px; */
    display: flex;
    justify-content: space-between;

}
.order-buttons__button-close{
    position: absolute;
    font-weight: 700;
    padding: 0;
}
.order-buttons__button-close:hover{
    background: rgba(255, 255, 255, 0.3);
    border-radius: 35px;
}
.order-buttons__button-close:active{
    background: rgba(255, 255, 255, 0.3);
    border-radius: 35px;
    color: rgba(0, 0, 0, 0.815);;
}
.order-buttons__button-return{
    text-align: center;
}

</style>