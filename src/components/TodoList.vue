<template>
    <div>
        <ul>
        <TodoItem v-for="(td, i) of todos" :key="td.id" 
        v-bind:td="td" v-bind:index="i" 
        v-on:remove-task="RemoveTask"
        v-on:edit-task="EditTask"
        v-on:done-task="ChangeDone"
            />
        </ul>
    </div>
</template>

<script>
    import TodoItem from '@/components/TodoItem'
    export default{
        props: ['todos', 'newtextTask'],
        components: {
            TodoItem
        },
        methods:{
            RemoveTask(id){
                this.$emit('remove-task', id)
            },
            EditTask(id, taskT){
                console.log(id);
                this.$emit('finish-edit-task', id, taskT)
            },
            ChangeDone(id){
                this.$emit('done-task', id)
            }
        }
    }
</script>

<style scoped>
ul{
    list-style: none;
    margin: 0;
    padding: 0;
    width : 60%;
}
div {
    display: flex;
    justify-content: center;
}

</style>