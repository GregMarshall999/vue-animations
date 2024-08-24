<template>
    <div class="todos">
        <input 
            type="text" 
            v-model="newTodo" 
            @keypress.enter="addTodo"
            placeholder="Ajoutez une tache..."
        />
        <div v-if="todos.length">
            <ul>
                <li v-for="todo in todos" :key="todo.id" @click="deleteTodo(todo.id)">
                    {{ todo.text }}
                </li>
            </ul>
        </div>
        <div v-else>Toutes les taches sont terminées!</div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            todos: [
                { text: 'Faire le lit', id: 1 }, 
                { text: 'Preparer le petit dej', id: 2 }
            ], 
            newTodo: ''
        }
    },
    emits: ['badValue'], 
    methods: {
        addTodo() {
            if(this.newTodo) {
                const id = Math.random();
                this.todos = [{ text: this.newTodo, id }, ...this.todos];
                this.newTodo = '';
            }
            else {
                this.$emit('badValue');
            }
        }, 
        deleteTodo(id) {
            this.todos = this.todos.filter(todo => todo.id != id);
        }
    }
}

</script>

<style>
input {
    width: 100%;
    padding: 12px;
    border: 1px solid #eee;
    border-radius: 10px;
    box-sizing: border-box;
    margin-bottom: 20px;
}

.todos {
    width: 400px;
    margin: 20px auto;
}

.todos ul {
    position: relative;
    padding: 0;
}

.todos li {
    list-style-type: none;
    display: block;
    margin-bottom: 10px;
    padding: 10px;
    background: white;
    box-shadow: 1px 3px 5px rgba(0, 0, 0, 0.1);
    border-radius: 10px;
    width: 100%;
    box-sizing: border-box;
}

.todos li:hover {
    cursor: pointer;
}
</style>