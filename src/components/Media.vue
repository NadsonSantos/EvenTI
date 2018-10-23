<template>
    <div> </div>
</template>
<script>
export default {
    
}
</script>
<style lang="scss">

@media screen and (max-width: 550px){
    .menu{
        display: none;
    };
    .menu2{
        display: inline-flex;
    }
    .btn{
        width: 48.4px ;
        height: 48px ;
        justify-content:center;
    };
    .local{
        margin-left: 78px ;
        margin-bottom: -49px ;
    };
    .conteudo{
        padding-left: 65px ;
        margin-left: 12px ;
        margin-top: -60px ;
    };
    .link{
        margin-right: 10px ;
    };
    .busca{
    justify-content: space-between;
    };
    .item-img{  
        width: 70px ;
        height: 105px ;
    };
    .imagem{
        width: 70px ;
        height: 105px ;
        object-fit: cover ;
    };
    .btn-img{
        display: block ;
    };
    .btn-p{
        display: none ;
    };
}
    
@media screen and (max-width: 500px){
    .items{
        width: auto ;
    };
    .entrada-img{
        display: none ;
    };
    .tags{
        display: none ;
    };
    .subtitulo{
        font-size: 16px;
        line-height: 2;
    };
    .entrada{
        line-height: 2.31;
        font-size: 13px;
    };
    .local{
        font-size: 9px;
        line-height: 2.22;
        letter-spacing: 0.1px;
    };
    .title{
        font-size: 12px;
        line-height: 2;
        letter-spacing: 0.1px;
    };
    .horario{
        font-size: 12px;
        letter-spacing: 0.1px;
        font-weight: 300;
    };
    .link{
        font-size: 12px;
        line-height: 2.08;
        width: 101px;
        height: 33px;
    };
    .heart{
        width: 16px;
        height: 14px;
    }
};
@media screen and (max-width: 960px){
    .tags{
        display: none ; 
    };
    .rodape{
        margin-left: 20px;
        justify-content: end ;
    }
}
</style>
