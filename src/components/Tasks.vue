<template>
    <div class="panel tasks">
        <Status :tasks="tasks"></Status>
        <TaskInput @onAddTask="addTask($event)"></TaskInput>
        <TaskList :tasks="tasks"></TaskList>

    </div>
</template>

<script>
import Status from '../components/Status'
import TaskInput from '../components/TaskInput'
import TaskList from '../components/TaskList'

export default {
    components: { Status, TaskInput, TaskList },
    data(){
        return {
            lastId: 0,
            tasks: []
        }
    },
    methods: {
        addTask(task){
            this.lastId++
            this.tasks.push({id: this.lastId, description: task.description, completed: false})
        },
        storageAvailable(type) {
            try {
                var storage = window[type],
                    x = '__storage_test__';
                storage.setItem(x, x);
                storage.removeItem(x);
                return true;
            }
            catch(e) {
                return e instanceof DOMException && (
                    // everything except Firefox
                    e.code === 22 ||
                    // Firefox
                    e.code === 1014 ||
                    // test name field too, because code might not be present
                    // everything except Firefox
                    e.name === 'QuotaExceededError' ||
                    // Firefox
                    e.name === 'NS_ERROR_DOM_QUOTA_REACHED') &&
                    // acknowledge QuotaExceededError only if there's something already stored
                    storage.length !== 0;
            }
        }
    },
    created(){
        if (this.storageAvailable('localStorage')) {
            if (localStorage.getItem('tasks')) {
                //console.log(localStorage)
                this.tasks = JSON.parse(localStorage.getItem('tasks'))

            } else {
                //console.log(localStorage.getItem('todoapp'))
            }

        } else {
            alert('seu browser não suporta salvar suas tarefas localmente!')
        }
    },
    watch: {
        tasks: {
            deep: true,
            handler: function() {
                if (this.storageAvailable('localStorage')) {
                    localStorage.setItem('tasks', JSON.stringify(this.tasks))
                }
            }
        }
    }
}
</script>

<style scoped>
.panel {
  width: 100%;
}
.tasks {
    display: grid;
    justify-items: center;
}
</style>
