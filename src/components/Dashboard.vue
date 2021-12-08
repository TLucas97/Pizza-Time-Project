<template>
                <Msg :msg="msg" v-show="msg" />
    <div id="pizza-table">
        <div>
            <div id="pizza-table-heading">
                <div class="id-order">#</div>
                <div>Cliente:</div>
                <div>Massa:</div>
                <div>Queijo:</div>
                <div>Molho:</div>
                <div>Adicionais:</div>

            </div>
        </div>
        <div id="pizza-table-rows">
            <div class="pizza-table-row" v-for="pizza in pizzas" :key="pizza.id">
                <div class="order-number">{{pizza.id}}</div>
                <div>{{pizza.nome}}</div>
                <div>{{pizza.massa}}</div>
                <div>{{pizza.queijo}}</div>
                <div>{{pizza.molho}}</div>
                <div>
                    <ul>
                        <li v-for="(adicional, index) in pizza.adicionais" :key="index">{{adicional}}</li>
                    </ul>
                </div>
                <div class="status">
                    <select name="status" class="status" @change="updatePizza($event, pizza.id)">
                        <option value="" disabled>Status</option>
                        <option v-for="actual in status" :key="actual.id" :value="actual.tipo" :selected="pizza.status == actual.tipo">{{actual.tipo}}</option>
                    </select>
                    <button class="btn-delete" @click="deletePizza(pizza.id)">Remover</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import Msg from './Msg.vue'

export default {
    name: 'Dashboard',
    data(){
        return{
            pizzas: null,
            pizza_id: null,
            status: [],
            msg: null
        }
    },
        components: {
        Msg
    },
    methods: {
        async makePedidos(){
            const req = await fetch("http://localhost:3000/pizzas")

            const data = await req.json();

            this.pizzas = data;

            //status
            this.makeStatus();

        },
        async makeStatus(){
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();

            this.status = data;
        },
        async deletePizza(id){
            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: 'DELETE'
            });

            const res = await req.json();

            this.msg = "Pizza removida com sucesso!"

            setTimeout(() => this.msg = "", 2000);

            this.makePedidos();
        },
        async updatePizza(event, id){

            const option = event.target.value;

            const dataJson = JSON.stringify({ status: option });

            const req = await fetch(`http://localhost:3000/pizzas/${id}`, {
                method: "PATCH",
                headers: {"Content-Type": "application/json"},
                body: dataJson
            });

            const res = await req.json();

            console.log(res);
        }
    },
    mounted(){
        this.makePedidos();
    }
}
</script>

<style scoped>

    #pizza-table{
        max-width: 1600px;
        margin: 0 auto;
    }

    #pizza-table-heading, #pizza-table-rows, .pizza-table-row{
        display: flex;
                flex-wrap: wrap;
    }

    #pizza-table-heading{
        font-weight: bold;
        padding: 12px;
        border-bottom: 3px solid #333;
        display: flex;
    }

    #pizza-table-heading div, .pizza-table-row div {
        width: 19%;
    }

    .pizza-table-row{
        width: 100%;
        padding: 12px;
        border: 1px solid #ccc;
    }

    #pizza-table-heading .id-order, .pizza-table-row .order-number{
        width: 5%;
    }

    select{
        padding: 10px 15px 10px 10px;
        border: 2px solid rgba(0, 0, 0, 0.479);
        margin-right: 12px;
        color: black;
        letter-spacing: 3px;
        font-size: .8rem;
    }

    .btn-delete{
        padding: 10px 10px;
        margin-top: .5em;
        border: 2px solid rgba(51, 51, 51, 0.507);
        background: rgba(255, 0, 0, 0.87);
        color: white;
        letter-spacing: 3px;
        font-size: .8rem;
        cursor: pointer;
    }

</style>