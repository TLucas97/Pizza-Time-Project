<template>
<div class="ma1n">
    <p>Monte sua pizza no seu estilo</p>  
    <Msg :msg="msg" v-show="msg" />
    <div id="arrow-bottom"><img :src="arrow" alt="arrow" id="arrow-down"></div>
    <div>
        <form id="pizza-form" @submit="make_pizza">
            <div class="input-style">
            <label for="nome">Nome do cliente:</label>
            <input type="text" id="nome" name="name" v-model="nome" placeholder="Digite seu nome!">
            </div>

            <div class="input-style">
            <label for="massa">Escolha o tipo da massa:</label>
            <select name="massa" id="massa" v-model="massa">
                <option value="" disabled>Selecione a massa</option>
                <option v-for="massa in massas" :key="massa.id" :value="massa.tipo">{{massa.tipo}}</option>
            </select>
            </div>

            <div class="input-style">
            <label for="queijo">Escolha o tipo de queijo</label>
            <select name="queijo" id="queijo" v-model="queijo">
                <option value="" disabled>Selecione o queijo</option>
                <option v-for="queijo in queijos" :key="queijo.id" :value="queijo.tipo">{{queijo.tipo}}</option>
            </select>
            </div>

            <div class="input-style">
            <label for="molho">Escolha seus molhos:</label>
            <select name="molho" id="molho" v-model="molho">
                <option value="" disabled>Selecione seu molho</option>
                <option v-for="molho in molhos" :key="molho.id" :value="molho.tipo">{{molho.tipo}}</option>
            </select>
            </div>

            <div class="input-style">
                <label for="adicionais">Escolha os adicionais:</label>
                <div class="flex">
                    <div class="checkbox-pizza" v-for="adicional in adicionaisdata" :key="adicional.id" >
                        <input type="checkbox" class="check" name="adicionais" v-model="adicionais" :value="adicional.tipo">
                        <span>{{adicional.tipo}}</span>
                    </div>
                </div>
            </div>

            <div class="input-style">
                <input type="submit" class="submit-btn" value="Criar minha pizza!">
            </div>
        </form>
    </div>
</div>
</template>

<script>
import Msg from './Msg.vue'

export default{
    name: 'PizzaForm',
    data(){
        return{
            arrow: './img/down-arrow.png',
            massas: null,
            queijos: null,
            molhos: null,
            adicionaisdata: null,
            nome: null,
            massa: null,
            queijo: null,
            molho: null,
            adicionais: [],
            msg: null
        }
    },
    methods: {
        async request_ingredients(){
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.massas = data.massas;
            this.queijos = data.queijos;
            this.molhos = data.molhos;
            this.adicionaisdata = data.adicionais;
        },

        async make_pizza(e){
            e.preventDefault();

            console.log("It's your pizza time!")

            const data = {
                nome: this.nome,
                massa: this.massa,
                queijo: this.queijo,
                molho: this.molho,
                adicionais: Array.from(this.adicionais),
                status: "Solicitado"
            }
            
            const dataJson = JSON.stringify(data);

            const req = await fetch("http://localhost:3000/pizzas", {
                method: "POST",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json();

            // msg de sistema - selecionando com this
            this.msg = `Pizza criada com sucesso!`

            // limpar carro com uma função setTime
            setTimeout(() => this.msg = "", 2000);

            this.nome = "";
            this.massas = "";
            this.queijos = "";
            this.molhos = "";
            this.adicionais = "";
            
        }
    },
    mounted(){
        this.request_ingredients()
    },
    components: {
        Msg
    }
}
</script>


<style scoped>
.ma1n{
    background: rgb(255, 255, 255);
    
}

p{
    text-align: center;
    font-size: 3rem;
    padding-top: .1em;
}

#arrow-bottom{
    display: flex;
    justify-content: center;
    align-items: center;
}

#arrow-down{
    margin-top: 1em;
    width: 50px
}

#pizza-form{
    margin: 0 auto;
    max-width: 35%;
}

.input-style{
    display: flex;
    flex-direction: column;
    margin-bottom: 1em;
}

.check{
    margin-top: .5em;
    margin-left: 1em;
}

span{
    font-size: 1.1rem;
    margin-left: .3em;
}

label{
    margin-bottom: .3em;
    font-weight: bold;
    font-size: 1rem;
    border-left: 7px solid gray;
    padding-left: .2em;
}

input{
    padding: .7em;
}

select{
    padding: .5em;
}

option{
    font-size: 1.5rem;
}

.submit-btn{
    cursor:pointer;
    border-radius: 10px;
    padding: .4em;
    background: #222;
    color: white;
    font-weight: bold;
    font-size: 1.5rem;
    transition: 1s;
}

.submit-btn:hover{
    color: rgb(255, 208, 0);
    letter-spacing: .2em;
}

.flex{
    display: flex;
    flex-direction: row;
}
</style>