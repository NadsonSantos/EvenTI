<template>
    <div class="m">
        <header class="cabecalho">
            <img class="logo" src="../assets/bitmap.jpg" alt="logo">
            <ul class="menu">
                <li> <a href="#"> Sobre nós</a></li>
                <li> <a href="#">Créditos</a></li>
                <li> <a href="#">Sugestão</a></li>
                <li> <a href="#"><img src="../assets/invalid2-name.png"></a></li>
                <li> <a href="#"><img src="../assets/group-7.png"></a></li>
            </ul>
            <!-- menu retratril  -->
            <div class="menu2" >   
                <a class="menu-btn"  @click.prevent="clicar(active)"><img src="../assets/icons-8-carda-pio.png" alt="menu" class="m-img" ></a>
                <div class="barra" v-bind:class="{ visible : active, hidden : !active }">
                    <div class="fechar">
                        <a class="btn-fechar" href="#" @click.prevent="clicar(active)">
                            <img src="../assets/close.png" alt="fechar">
                        </a>
                    </div>
                    <nav >

                        <ul class="menu-lista"> 
                            <li class="m-link" v-bind:class="{ fadeleft : active}" ><a href="#" class="link-container"> Sobre nós</a> </li>
                            <li class="m-link" v-bind:class="{ fadeleft2 : active}"><a href="#" class="link-container">Créditos</a></li>
                            <li class="m-link" v-bind:class="{ fadeleft3 : active}"><a href="#" class="link-container">Sugestão</a></li>
                            <!-- <li class="m-link">
                                <a class="link-container menu2-img" href="#">
                                    <img src="../assets/invalid2-name.png">
                                </a>
                            </li>
                            <li class="m-link">
                                <a class="link-container menu2-img" href="#">
                                    <img src="../assets/group-7.png">
                                </a>
                            </li> -->
                        </ul>  
                    </nav>
                </div>
            </div>
        </header>
    </div> 
</template>
<script>
export default {
    data(){
        return{
            active : false,
        }
    },
    methods:{
        clicar : function(active){
            this.active = !this.active;
            return active
        },
    }
}
</script>
<style lang="scss">
    @keyframes menu {
        from {
            opacity: 0;
            transform: translate3d(-100%, 0, 0);
        }

        to {
            opacity: 1;
            transform: translate3d(0, 0, 0);
        }
    }
    .fadeleft{
        animation: menu 200ms 0s ease-in-out;
    }
    .fadeleft2{
        animation: menu 300ms 0s ease-in-out;
    }
    .fadeleft3{
        animation: menu 400ms 0s ease-in-out;
    }
    .cabecalho{
        margin-left: 30px;
        margin-bottom: 20px;
        padding-top: 20px;
        display: flex;
        justify-content: space-between;
    };
    .logo{
        animation: fadeIn 0.9s  ease-in-out;
        width: 66px;
        height: 31px;
    };

    .menu{
        align-items: center;
        overflow: hidden;
        animation: fadeIn 0.9s ease-in-out;
        display: inline-flex;
        margin-top: 0;
        list-style: none;
        li{     
            display: inline-block;
            margin-right: 29px;
            a{
                text-decoration: none;
                color: black;
                img{
                    padding-top:6px;
                    width: 25px;
                    height: 25px;
                }
            }
        }
    };
    .menu-retratil{
        margin-right: 30px;
        width: 26px;
        height: 18px;
        background-color: #fff;
    };
    .m-img{
        width: 26px;
        height: 18px;
        object-fit: contain;
    };
    .menu-retratil{
        display: none;

    };
    .menu-btn{
        background: none;
        z-index: 0;
        margin-right: 20px;
    }
    .barra{
        animation: fadeIn 200ms ease-in-out;
        display: inline-flex;
        justify-content: center;
        overflow: hidden;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        position: fixed;
        background-color: #000;
        transition: all .25s linear;
        z-index: 10;
        align-items: center;

    };
    .menu2{
        display: none;
    };
    .menu-lista{
        display: flex;
        flex-direction: column;
        align-items: center;
    };
    .link-container{
        display: flex;
        align-items: center;
        text-decoration: none;
        color: #fff;
        padding-bottom: 20px;
        font-size: 26px;
    }
    .menu2-img{
        width: 30px;
        height: 30px;
        img{
            background-color: #fff;
            width: 100%;
            height: 100%;
        }
    }

    .visible {
        visibility: visible;
        opacity: 1;
        transition: opacity 250ms ease-in-out;
    }
    
    .hidden {
        visibility: hidden;
        opacity: 0;
        transition: visibility 0s 200ms, opacity 250ms ease-in-out;
    }
    .fechar{
        display: block;
        position: absolute;
        top: 0;
        right: 0;
        padding-right: 20px;
        padding-top: 20px;
    }
    .btn-fechar{
    }
</style>

