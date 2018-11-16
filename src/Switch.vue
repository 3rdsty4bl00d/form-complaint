<template>
    <div>
        <div id="on" @click="switched(true)" :class="active = value">
            On
        </div>
        <div id="off" @click="switched(false)" :class="active = !value">
            Off
        </div>
    </div>
</template>


<script>
    export default {
        props: ['value'],
        methods: {
            switched(isOn) {
                this.$emit('input', isOn);
            }
        }
    }
</script>


<style>
    #on, #off {
        width: 40px;
        height: 20px;
        background-color: lightgray;
        padding: 2px;
        display: inline-block;
        margin: 10px -2px;
        box-sizing: content-box;
        cursor: pointer;
        text-align: center;
    }
    
    #on {
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
    }
    
    #off {
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }

    #on:hover, #on.active {
        background-color: lightgreen;
    }

    #off:hover, #off.active {
        background-color: lightcoral;
    }
</style>