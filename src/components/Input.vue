<template>
    <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Input number"> <br>
    <button @click="convert()">Exchange</button>
    <button @click="favourite()" class="fav-button">Favourite</button>

</template>
<script>
export default {
    data() {

    },

    props: {
        changeAmount: {
            type: Function,
            required: true
        },
         convert: {
            type: Function,
            required: true
        },
        favourite: {
            type: Function,
            required: true
        }
    }
};
</script>
<style scoped>
input{
    border-radius: 3px;
    border: 0;
    padding: 10px 15px;
    background: #fff;
    color: black;
    outline: none;
    width: 500px;
    margin-top: 80px;
    font-size: 1.2em;
}
button {
    margin-top: 25px;
    width: 100px;
    height: 40px;
    border: none;
    border-radius: 3px ;
    background: #ecf6bf;
    cursor: pointer;
    box-shadow: #6496e1 2px 2px 5px;
    font-size: 1em;
}
button:hover{
    background: #6496e1;
       box-shadow: #ecf6bf 2px 2px 5px;
       color:#fff
}

button.fav-button {
    margin-left: 20px;
}
</style>
