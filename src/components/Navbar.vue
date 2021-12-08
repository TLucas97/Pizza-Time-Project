<template>
<div id="nav">
    <router-link to="/" id="logo-place">
        <img :src="logo" :alt="alt" id="logo">
        <img :src="img" alt="pizza-time2" id="logo2">
        <img :src="logo" :alt="alt" id="logo">
        <div id="pizza-title"><h1>Pizza Time <span id="heart">♥</span></h1></div>
    </router-link>
    <div id="nav-links">
    <router-link to="/">home</router-link> <span>|</span>
    <router-link to="/pedidos">Pedidos</router-link>
    </div>
</div>
</template>

<script>
export default{
    name: "Navbar",
    props: ["logo", "alt"],
    data(){
        return{
            img: './img/pizza-time.png'
        }
    }
}

</script>

<style scoped>
#logo-place{
    display: flex;
    align-items: center;
}

#logo{
    width: 100px;
}

#logo2{
    width: 190px;
    border-radius: 40%;
}

#nav{
    display: flex;
    justify-content: flex-end;
    align-items: center;
    background: rgb(163, 51, 51);
    padding: .5em;
}

span{
    font-size: 1.5rem;  
    color: white;
}

#nav a{
    text-decoration: none;
    font-size: 1.5rem;
    padding-right: 1.5em;
    padding-left: 1.5em;
    color: white;
    text-transform: uppercase;
    letter-spacing: .5em;
    transition: .2s
}

#nav a:hover{
    color: rgba(255, 255, 255, 0.281);
}

#logo-place{
    margin: auto;
    margin-left: 0;
}

#nav-links{
    padding-right: 2em;
}

#pizza-title{
    margin-left: 2em;
    color: white;
    text-transform: capitalize;
}

</style>