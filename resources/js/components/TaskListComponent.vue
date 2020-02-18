<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <h6>Liste des tâches</h6>
                <ul class="list-group mb-3">
                    <li class="list-group-item" v-for="task in tasks">
                        {{ task.name }} - {{ task.status }}
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                tasks: []
            }
        },

        created() {
            axios.get('./api/tasks')
                .then((response) => this.tasks = response.data)

            Event.$on('taskCreated', (name) => {
                this.tasks.push(name)
            });
        }
    }
</script>
