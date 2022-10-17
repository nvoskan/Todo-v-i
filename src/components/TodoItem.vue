<template>
<li> 
    <span>
        <div class="tasktext"> 
            <div class = "child"> {{index + 1}}.)</div><div class = "child" v-bind:class="{'done': td.completed, 'disp-n': startEdit}">{{td.text}}</div>
            <input v-model="newTaskTxt" v-bind:class = "startEdit ? '' : 'disp-n'" class="texteditor" @change="$emit('edit-task', td.id, newTaskTxt)" type = "textarea" >
        </div>
        <div >
            <button class = "bttn" v-on:click="td.completed = !td.completed; $emit('done-task', td.id)">&#128505;</button>
            <button class = "bttn" v-on:click="StartEdit">&#9998;</button>
            <button class = "bttn" v-on:click="$emit('remove-task', td.id)">&#128465;</button>
        </div>
    </span>

</li>
</template>

<script>
export default{
    props:{
        td:{
            type: Object,
            required: true
        },
        index: Number
    },
    data(){
        return{
            newTaskTxt: '',
            startEdit: false
        }
    },
    methods:{
        StartEdit(){
            this.startEdit = !this.startEdit;
            this.showTask()
        },
        showTask(){
            this.newTaskTxt = this.td.text;
        }
    }
    
}
</script>

<style scoped>
    li{
        border: 1px solid rgb(76, 99, 72);
        background-color: rgb(237, 238, 234);
        display : flex;
        padding: .5rem 2rem;
        margin-bottom: 1rem;
        width: 90%;
    }
    .tasktext{
        display: inline-flex;
        width: 80%;
        margin: 10px;
    }
    .texteditor{
        width: 100%;
    }
    .child{
        padding: 5px;
        margin: 5px;
    }
    span {
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        align-content: center;
        text-align: left;

    }
    .bttn{
        margin-top: 10px;
        margin-right: 3px;
        text-align: center;
        font-size: 1.5vw;
        padding: 0.1em;
        justify-content: center;
        width: 2.5vw;
        height: 2.5vw;
        border: 1px solid rgb(76, 99, 72);
        border-radius: 20%;
    }
    input{
        margin-right:1rem;
    }
    .done {
        text-decoration: line-through;
        text-decoration-thickness: 2px;
    }
    .disp-n{
        display:none
    }
</style>