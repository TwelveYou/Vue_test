<template>
    <div className="complited-order">
        <div className="complited-order-wrap">
            <h1 className="complited-order__text">Ваш заказ успешно оформлен. Вам перезвонит оператор в ближайшее время</h1>
            <button
                className="complited-order__button-close"
                @click="this.$emit('closeComplitedOrderMessage')"
            >Вернутся</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ComplitedOrderMessage'
}
</script>

<style>
    .complited-order{
        position: fixed;
        top: 0;
        left: 0;

        height: 100vh;
        width: 100vw;

        background-color: rgba(0, 0, 0, 0.9);
        color: white;
        text-align: center;

        display	: table;
    }
    .complited-order-wrap{
        display	: table-cell;
        vertical-align : middle;
    }
    .complited-order__text{
        width: 70%;
        margin:0 auto 20px;
    }
</style>