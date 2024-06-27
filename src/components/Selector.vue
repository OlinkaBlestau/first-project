<script>
export default {
    props: {
        setCrypto:{
            type: Function,
            required: true
        }
    },
    data(){
        return {
           current: '' 
        }   
    },
    methods:{
        selectItem(val){
            this.setCrypto(val);
            this.current = val
        }
    }
};
</script>

<template>
  <ul>
    <li @click="selectItem('BTC')" :class="current == 'BTC' ? 'active' : ''" >Bitcoin</li>
    <li @click="selectItem('ETH')" :class="current == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="selectItem('USDT')" :class="current == 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<style scoped>
ul {
    margin: 50px 10px;
    list-style: none;
    width: 200px;
    border-radius: 3px;
    border: 3px solid #4331c784;
}
li{
    display: block;
    background: #8377c58c;
    color: #fff;
    padding: 20px 0;
}
li:hover, li.active{
    background: #433551;
    cursor: pointer;
  
}
</style>
