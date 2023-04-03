<template>
    <div className="header">
        <div className="header-content">
            <p class="header-content__logo"><span>Вкусная</span> Пицца</p>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'HeaderOfApp',
    }   
</script>

<style>
@media (min-width: 1200px){
    .header-content{
        width: 1100px;
    }
}
@media (min-width: 992px) and (max-width: 1199.99px) {
    .header-content{
        width: 920px;
    }    
}
@media (min-width: 700px) and (max-width: 991.99px) {
    .header-content{
        width: 570px;
    }    
}  
@media (max-width: 699.99px) {
    .header-content{
        width: 300px;
    }    
    .header-content__logo{
        text-align: center;
    }
} 

.header{
    height: 100px;
    background: url('../assets/header-pattern.jpg') repeat center , #444444;
    background-blend-mode: hard-light;
}
.header-content{
    margin:auto;
}
.header-content__logo{
    font-size: 32px;
    font-weight: 700;
    padding-top: 28px;
    color: white;
}
.header-content__logo > span{
    color: rgb(255, 30, 0);
}
</style>