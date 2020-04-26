<template>
    <div
        v-if="tasks.length"
        class="panel task-list"
    >
        <div
            v-for="(task, index) in tasks"
            :key="task.id"
            class="task"
            :class="{ completed: task.completed}"
        >
            <div
                class="task-text"
                :class="{ 'completed-text': task.completed }"
                @click="task.completed = !task.completed"
            >
                {{ task.description }}
            </div>
            <div
                class="btn-delete"
                @click="tasks.splice(index, 1)"
            >
                <span>X</span>
            </div>
        </div>
    </div>
    <div
        v-else
        class="panel"
    >
        <p>Uau! Você não tem nenhuma tarefa!</p>
    </div>
</template>

<script>
export default {
    props: {
        tasks: {
            type: Array,
            default: () => {
                return []
            }
        }
    }
}
</script>

<style scoped>
.panel {
    width: 100%;
}
.task-list {
    display: grid;
    justify-items: center;
    grid-gap: 5px 5px;
    margin-top: 5px;
}
.task {
    display: grid;
    grid-template-columns: 1fr 48px;
    grid-template-rows: repeat(auto-fit, minmax(auto, auto));
    width: 100%;
    align-items: center;
    background-color: #ff3366;
    border-radius: 10px;
}
.completed {
    background-color: #2ac940;
}
.completed-text {
    text-decoration: line-through;
}
.task-text {
    font-weight: 300;
    color: #fff;
    text-align: left;
    padding: 16px 16px;
}
.btn-delete {
    font-weight: 300;
    color: #fff;
    width: 48px;
    height: 48px;
    display: grid;
    align-items: center;
}

@media (min-width: 768px) {
    .task-list {
        grid-template-columns: repeat(auto-fit, minmax(200px, auto));
        justify-content: center;
        justify-items: center;
    }
    .task {
        height: 100px;
    }
}
</style>
