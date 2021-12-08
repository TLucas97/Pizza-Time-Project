<template>
<div class="container-msg">
    <p>{{ msg }}</p>
</div>
</template>

<script>
export default{
    name: 'Msg',
    props: {
        msg: String
    }
}
</script>

<style scoped>
.container-msg{
    padding: 1em;
    text-align: center;
    background: rgb(163, 51, 51);
    border: rgba(0, 0, 0, 0.342) 2px solid;
    border-radius: 20px 0px 20px 20px;
    width: 300px;
    margin: 0 auto;
    color: rgba(255, 254, 254, 0.658);
    opacity: .7;
}

</style>
