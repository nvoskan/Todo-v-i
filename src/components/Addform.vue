<template>
<div class = "container">
    <form @submit.prevent="onSubmit">
        <input type = "text" v-model="text">
        <button type = "submit">Добавить</button>
    </form>
</div>
</template> 

<script>
export default{
    data(){
        return{
            text: ''
        }
    },
    methods: {
        onSubmit(){
            if (this.text.trim()){
                const newtask = {
                    id: Date.now(),
                    text: this.text,
                    completed: false
                }
            this.$emit('add-task', newtask)
            this.text = ''
            }
        }
    }
}

</script>

<style scoped>
.container{
    width: 60%;
    margin-left: auto;
    margin-right: auto;
    
}
form{
    height: 2.5vw;
    display : flex;
    padding: .5rem 2rem;
    margin-bottom: 1rem;
    width: 90%;
    background-color: rgb(76, 99, 72);
    justify-content: space-between;
    align-content: center;
}
input{
    margin-left: 5%;
    width: 70%;
}
button{
    min-width: 15%;
    font-size: medium;
}
</style>