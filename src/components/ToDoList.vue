<template>
    <div>
        <ul>
            <ToDoItem 
                v-for="(todo, i) of todos"
                v-bind:index='i'
                v-bind:todo='todo'
                :key='todo.id'
                v-on:remove-todo='removeToDo'
            />
        </ul>
    </div>
</template>

<script>
import ToDoItem from '@/components/ToDoItem'
export default {
    props: ['todos'],
    components: {
        ToDoItem
    },
    methods: {
        removeToDo(id) {
            this.$emit('remove-todo', id)
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>