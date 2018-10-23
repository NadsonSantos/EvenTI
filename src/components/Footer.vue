<template>
    <div class="f" >
        <footer class="rodape">
            <div class="rodape-container">
                <img src="../../src/assets/bitmap2.jpg" alt="logo" class="rodape-img">
                <p> &#169; EvenTI - Eventos de TI</p>
            </div>
            <div class="r-vazio"></div>
        </footer>
    </div>
</template>
<script>
export default {
}
</script>
<style lang="scss">
    .rodape{
        justify-content:space-around;
        display: flex;
        align-items: center;
        color:  #767676;
        margin-bottom: 23px;
        margin-top: 22px;
    };
    .rodape-container{
        display: flex;
        align-items: center;
        justify-content:left;
        img{
            width: 46px;
            height: 22px;
        }
        p{
            font-size: 15px;
            color: #767676;
            line-height: 1.2;
        }
    };
    .rodape-img{
        padding-right: 16px;
    };
    .r-vazio{
        width: 10px;
        display: flex;
    }
</style>


