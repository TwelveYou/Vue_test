<template>
    <div className="footer">
        <div className="footer-content">
            <p className="footer-content__text">Кушайте вкусно!</p>
        </div>
    </div>
</template>

<script>
    export default{
        name: 'HeaderOfApp',
        data() {
            return{
                test: 0
            }
        }
    }   
</script>

<style>
@media (min-width: 1200px){
    .footer-content{
        width: 1100px;
    }
}
@media (min-width: 992px) and (max-width: 1199.99px) {
    .footer-content{
        width: 920px;
    }    
}
@media (min-width: 700px) and (max-width: 991.99px) {
    .footer-content{
        width: 570px;
    }    
}  
@media (max-width: 699.99px) {
    .header-content{
        width: 300px;
    }    
} 
.footer{
    height: 100px;
    background: url('../assets/header-pattern.jpg') repeat center , #444444;
    background-blend-mode: hard-light;
}
.footer-content{
    margin:auto;
}
.footer-content__text{
    font-size: 16px;
    padding-top: 35px;
    color: white;
    text-align: center;
}
</style>