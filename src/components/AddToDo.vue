<template>
    <form class="form" @submit.prevent='onSubmit'>
        <div class="add-todo">
            <input class="add-todo__input" type="text" v-model='title'>
            <button class="add-todo__button" type="submit">Add</button>
        </div>
    </form>
</template>

<script>
export default {
    data() {
        return {
            title: ''
        }
    },
    methods: {
        onSubmit() {
            if (this.title.trim()) {
                const newToDo = {
                    id: Date.now(),
                    title: this.title,
                    completed: false
                }
                this.$emit('add-todo', newToDo)
                this.title = ''
            }
        }
    }
}
</script>

<style scoped>
    .form {
        display: flex;
    }
    .add-todo {
        display: flex;
        justify-content: center;
        flex-basis: 100%;
        margin: 20px 0 20px;
    }
    .add-todo__input {
        display: flex;
        max-width: 600px;
        font-size: 16px;
        padding: 10px;
        padding-left: 20px;
        border-radius: 20px;
        outline: none;
        border: 1px solid #2c3e50;
    }
    .add-todo__button {
        cursor: pointer;
        display: flex;
        justify-content: center;
        align-items: center;
        width: 36px;
        height: 36px;
        background: #fff;
        border: 1px solid #2c3e50;
        border-radius: 18px;
        margin-left: 10px;
        outline: none;
    }

</style>