<template>
    <button :class="state" v-on:click="clickButton()">
        <span v-if="state=='delete'"><em class="far fa-trash-alt"></em></span>
        <span v-else><em class="fas fa-plus"></em></span>       
    </button>
</template>
<script>
export default {
    name:"myButton",
    props:['state'],
    data(){
        return{
            
        }
    },
    emits:['added','deleted'],
    methods:{
        clickButton(){
            console.log('button is clicked');
            if(this.state=='delete'){
                this.$emit("deleted")
            }
            if(this.state=='add'){
                this.$emit("added")
            }

        }

    }
}
</script>
<style>
    @import 'https://cdn.jsdelivr.net/npm/bootstrap@5.0.0-beta3/dist/css/bootstrap.min.css';
    @import 'https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.3/css/all.min.css';
    button{
        border: 2px solid black;
        width: 80px;
        height: 48px;
    }
    .delete{
        background-color: rgb(241, 90, 90);
    }
    .add{
        background-color: rgb(135, 135, 245);
    }

</style>