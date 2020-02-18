<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <form action="./api/tasks" method="POST" @submit.prevent="addTask()">
                    <div class="form-group">
                        <label for="task">Nom de la tâche</label>
                        <input type="text" class="form-control" v-model="name" id="task" name="name">
                        <div class="text-danger" v-for="error in errors">{{ error[0] }}</div>
                    </div>
                    <button type="submit" class="btn btn-primary">Ajouter la tâche</button>
                </form>
            </div>
        </div>
    </div>
</template>

<script>

    export default {
        data() {
            return {
                'name': '',
                'errors': {}
            }
        },

        methods: {
            addTask() {
                axios.post('./api/tasks', {
                    name: this.name
                }).then((response) => {
                    Event.$emit('taskCreated', {name: this.name})
                    this.name = '';
                }).catch((error) =>
                    this.errors = error.response.data.errors
                )}
        }
    }
</script>
