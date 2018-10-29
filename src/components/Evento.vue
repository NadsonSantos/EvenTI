<template>
    <main class="app">
        <div class="container">
            <h1 class="titulo">EvenTI</h1>
            <h2 class="subtitulo">
                    Agregador para quem   <img src="../../src/assets/invalid-name.png" alt="coração" class="heart">   eventos de TI <br>em salvador e região
            </h2>
            <div class="busca">
                <img src="../../src/assets/magnifier-simple-line-icons.png" class="entrada-img"  alt="buscar">
                <input type="text" class="entrada" v-model="search" placeholder="Localize um evento" @keyup.enter="onSearch">
                <button class="btn" v-on:click="onSearch">
                    <img src="../../src/assets/magnifier-simple-line-icons-white.png" alt="buscar" class="btn-img">
                    <p class="btn-p"> Buscar</p>
                </button>
            </div>
            <p class="secao">Hoje</p>
            <ul class="lista">
                    <li class="items" v-for="item in hj" v-bind:key="item.id">
                        <p class="local"> {{item.locale}}</p>
                        <div class="item-img"><img :src=" item.image || img_default " alt="" class="imagem"></div>
                        <div class="conteudo">
                            <p class="title"> {{item.title}} </p>
                            <p class="horario">
                                {{formatStart(item.date_start, item.hour_start )}}
                                {{formatEnd(item.date_end, item.hour_end)}}
                            </p>
                            <!-- <div class="tags">
                                <p class="tag">arduino</p>
                                <p class="tag">Jogos</p>
                                <p class="tag">Banco de dados</p> 
                            </div> -->
                            <div class="item-link">
                                <a :href=" item.link " target="_blank" class="link"> ver evento </a>
                            </div>
                        </div>
                    </li>
            </ul>
            <p class="secao">Próximos Eventos</p>
            <ul class="lista">
                <li  class="items" v-for="item in items" v-bind:key="item.id">
                    <p class="local"> {{item.locale}}</p>
                    <div class="item-img"><img :src=" item.image || img_default " alt="" class="imagem"></div>
                    <div class="conteudo">
                        <p class="title"> {{item.title}} </p>
                        <p class="horario">
                            {{formatStart(item.date_start, item.hour_start )}}
                            {{formatEnd(item.date_end, item.hour_end)}}
                        </p>
                        <!-- <div class="tags">
                            <p class="tag">arduino</p>
                            <p class="tag">Jogos</p>
                            <p class="tag">Banco de dados</p> 
                        </div> -->
                        <div class="item-link">
                            <a :href=" item.link " target="_blank" class="link"> ver evento </a>
                        </div>
                    </div>
                </li> 
            </ul>
            <div v-bind:class="{carregamento : load , vazio : !load}">
                <div class="load-img"><img src="../../src/assets/loading.gif" class="load-img" alt="logo"></div>
                <div class="load-p"><p>Carregando mais…</p></div>
            </div>
        </div>
    </main>
</template>
<script>
import Vue from 'vue';
import moment from 'moment';
import 'moment/locale/pt-br';
import axios from 'axios';

Vue.use(axios);
Vue.use(moment);

import img from '../assets/default.png';

export default {
    data(){
        return {
            img_default : img,
            hj : [],
            config: [],
            items: [],
            search: null,
            uri: 'https://guarded-oasis-77929.herokuapp.com/api/event',
            load : true,
        }
    },
    methods:{
        more : function(value) {
            if(value.length >= 15) {
                // this.config = response.data.data;
                let uri = this.uri + this.config.next_page_url;
                if (this.search !== null) {
                    uri = uri + '&search=' + this.search;
                    this.loading(this.config);
                }
                 axios.get(uri).then(response => {
                    if (response.data) {

                        this.config = response.data.data;
                        let item = response.data.data.data;
                        let temporario = response.data.data.data;
                        let today = moment(new Date()).format('YYYY-MM-DD');
                        item.forEach(data => {
                            this.items.push(data);
                        });
                        this.items = temporario.filter((value ) => {
                            if(value.date_start === today) {
                                this.hj.push(value);
                            }else{
                                return value
                            }
                        })
                    }
                })
            }
        },
        loading : function(value){
            if(value.next_page_url != null){
                return this.load = true 
            }else{
                return this.load = false
            }
        },
        onSearch: function () {
            if(this.search !== null){
                this.hj = [];
                this.items = [];
                const uri = this.uri + '?search=' + this.search;
                axios.get(uri).then(response => {
                    this.config = response.data.data;
                    let temporario = response.data.data.data;
                    let today = moment(new Date()).format('YYYY-MM-DD');
                    this.items = temporario.filter((value) => {
                        if(value.date_start === today) {
                            this.hj.push(value);
                        }else{
                            return value
                        }
                    })
                    this.loading(this.config);
                });
            }else{
                return 
            }
        },
        formatDate: function (date) {
            if (date === null) {
                return ' ';

            } else {
                return moment(date, 'YYYY-MM-DD').format('DD/MM/YYYY') + ", ";

            }
        }, formatHour: function (hour) {
            if (hour === null) {
                return ' '
            } else {
                return moment(hour, 'HH:mm:ss').format('HH:mm') + "h";
            }
        },
        formatStart: function (date, hour) {
            moment.locale();
            return moment(date, 'YYYY-MM-DD').format('LL') + ", " + moment(hour, 'HH:mm:ss').format('HH:mm') + "h";
        },
        formatEnd: function (date, hour) {
            if (date === null) {
                return '- ' + moment(hour, 'HH:mm:ss').format('HH:mm') + "h";
            } else if (hour === null) {
                return '- ' + moment(date, 'YYYY-MM-DD').format('LL');
            } else if (date == null && hour == null) {
                return " ";
            } else {
                return '- ' + moment(date, 'YYYY-MM-DD').format('LL') + ", " + moment(hour, 'HH:mm:ss').format('HH:mm') + "h";
            }
        },
        getInitialUsers() {
            axios.get(this.uri).then(response => {
                this.config = response.data.data;
                let temporario = response.data.data.data;
                let today = moment(new Date()).format('YYYY-MM-DD');
                this.items = temporario.filter((value ) => {
                    if(value.date_start === today) {
                        this.hj.push(value);
                    }else{
                        return value
                    }
                });
                this.loading(this.config);
                this.more(this.hj);
                // this.imagem(this.items.image);
            });
        },
        beforeMount() {
            this.getInitialUsers();
        },
        scroll() {
            let active = false;
            window.onscroll = () => {
                if (this.items.length == 0) {
                    return null;
                }
                let bottomOfWindow = window.scrollY + window.innerHeight  + 250 >= document.documentElement.offsetHeight ;
                if (bottomOfWindow && !active) {
                    active = true;
                    let uri = this.uri + this.config.next_page_url;
                    if (this.search !== null) {
                        uri = uri + '&search=' + this.search;
                    }
                    axios.get(uri).then(response => {
                        if (response.data) {
                            this.config = response.data.data;
                            let item = response.data.data.data;
                            item.forEach(data => {
                                this.items.push(data);
                            });
                        }
                        active = false;
                    });
                    // if(this.config.next_page_url != null){
                    //     return this.load = true 
                    // };
                    this.loading(this.config);
                }
            }
        },
    },
    mounted() {
        this.scroll(this.item);
    },
    created: function () {
        this.getInitialUsers();
    },   
}
</script>
<style lang="scss">
    .app{
        padding-right: 20px;
        padding-left: 20px ;
        align-items: center;
        flex-direction: column;
        display: flex;
        justify-content: center;
        margin-top: 114px;
    };
    .container{
        justify-content: center;
        flex-direction: column;
        display: flex;
        max-width: 1000px;
        border-bottom: 1px solid #dbdbdb;
    }
    .titulo{
        color: #5e72e4;
        font-size: 45px;
        font-weight: 600;
        display: block;
    };
    .subtitulo{
        font-size: 43px;
        font-weight: 500;
        line-height: 1.3;
        color: #484848;
    };
    .heart{
        width: 34px;
        height: 29px;
        object-fit: contain;
    };
    .busca{
        padding: 0px 12px 0 21px;
        margin-top: 30px;
        height: 72px;
        align-items: center;
        border-radius: 5px;
        background-color: #ffffff;
        box-shadow: 0 0 30px 0 #ececec;
        display: inline-flex;
    };
    .btn{
        display: inline-flex;
        width: 95px;
        height: 48px;
        line-height: 1.32;
        font-size: 19px;
        font-weight: 500;
        background-color: #5e72e4;
        border-radius: 5px;
        justify-content: center;
        cursor : pointer;
    };
    .btn-img{
        display: none;
    };
    .btn-p{
        display: block;
        color: #fff;
    };
    .entrada{
        outline: none;
        width: 100%;
        margin: 0px 17px;
        font-size: 19px;
        color: #767676;
        :hover{
            border: 0px;
        }
        
    };
    .entrada-img{
        display: inline-block;
        width: 24.1px;
        height: 24px;
        margin-bottom: -5px;
    };
    .secao{
        margin-top: 100px;
        margin-bottom: 30px;
        color: #484848;
        font-size: 26px;
        font-weight: 600;
        letter-spacing: 0.2px;
        color: #484848;
    };
    .carregamento{
        display: inline-flex;
        flex-direction: column;
        margin-top: 80px;
        display: inline-flex;
        justify-content: center;
        align-items: center;
        margin-bottom: 270px;
    };
    .vazio{
        display: none;
    };
    .load-img{
        display: inline-flex;
        width: 97px;
        height: 97px;
    };
    .load-p{
        color: #767676;
        font-size: 13px;
        display: inline-flex;
        justify-content: center;
    };
    .lista{
        display: flex;
        flex-direction: column;
    };
    .items{
        display:inline-block;
        margin: 50px 0px; 
        list-style: none;
    };
    .conteudo{
        padding-right: 10px;
        margin-left: 88px;
        padding-left: 187px;
        margin-top: -140px;
        padding-bottom: 22px;
        border-radius: 5px;
        background-color: #ffffff;
        box-shadow: 0 0 50px 0 #efefef;
    };
    .item-img{
        width: 240px;
        height: 187px;
        display: inline-flex;
        border-radius: 10px;
    }
    .imagem{
        display: inline-flex;
        width: 240px;
        height: 187px;
        border-radius: 10px;
        object-fit: fill;
    };
    .local{
        padding-right: 10px;
        margin-left: 275px;
        margin-bottom: -40px;
        line-height: 1.82;
        letter-spacing: 0.1px;
        color: #002b37;
        font-size: 11px;
        font-weight: 600;
    };
    .title{
        font-size: 24px;
        font-weight: 600;
        line-height: 1.67;
        letter-spacing: 0.2px;
        color: #464646;
        margin-bottom: 10px;
        padding-top: 16px;
    };
    .horario{
        margin-bottom: 22px;
    };
    .item-link{
        display: flex;
        justify-content: flex-end;
    };
    .link{
        display: inline-flex;
        justify-content: center;
        align-items: center;
        width: 139px;
        height: 48px;
        border-radius: 5px;
        background-color: #5e72e4;
        color: #ffffff;
        font-size: 19px;
        font-weight: 500;
        text-decoration: none;
        margin-right: 64px;
    };
    .tags{
        display: none;
        margin-top: 22px;
        justify-content: center;
        display: inline-flex;
        flex-direction: row;
    };
    .tag{
        display: none;
        margin-right: 19px;
        border-radius: 13px;
        background-color: #ff5661;
        letter-spacing: 0.1px;
        color: #ffffff;
        padding: 5px 15px;
    };
</style>
