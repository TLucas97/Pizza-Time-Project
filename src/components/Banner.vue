<template>
<div id="pizza-background">
    <div class="title2">
        <h2><a href="#pizza-form">Monte sua pizza!</a></h2>
        <div id="arrow-bottom"><img :src="arrow_1" alt="arrow" id="arrow-down"></div>
    </div>
</div>
</template>

<script>

export default{
    name: 'Banner',
    data(){
        return{
            arrow_1: '../img/down-arrow.png'
        }
    }
}
</script>

<style scoped>
#pizza-background{
    background: url('/img/pizza.jpg');
    background-position: center;
    background-size: cover;
    height: 850px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
}

#pizza-background h2 a{
    color: white;
    font-size: 5rem;
    margin-right: .5em;
    text-decoration: none;
    font-weight: 400;
}

#pizza-background h2 a:hover{
    font-weight: bold;
}

.title2{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    margin: 0 auto;
}
</style>