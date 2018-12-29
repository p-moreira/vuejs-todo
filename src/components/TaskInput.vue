<template>
    <div class="panel task-input">
        <input
            type="text"
            placeholder="O que deseja fazer?"
            @keyup.enter="addTask"
            v-model="taskInput"
        >
        <div class="btn-input" @click="addTask()">
            <span>+</span>
        </div>
    </div>
</template>

<script>

export default {
    data(){
        return {
            taskInput: ''
        }
    },
    methods: {
        addTask(){
            if (this.taskInput) {
                this.$emit('onAddTask', { description: this.taskInput })
                this.taskInput = ''
            }
        }
    }
}
</script>

<style scoped>
.panel {
  width: 100%;
}
.task-input {
    height: 48px;
    display: grid;
    grid-template-columns: 1fr 48px;
    align-items: center;
    margin: 15px 0;
}
.task-input input {
    border: 1px solid #e0e0e0;
    border-radius: 10px 0 0 10px;
    height: 100%;
    padding: 10px;
    font-size: 20px;
    font-weight: 100;
    box-sizing: border-box;
}
.task-input input:focus {
    outline: 0px;
    box-shadow: 0 0 10px rgba(50,50,50,0.1);
}
.btn-input {
    background-color: #3399ff;
    color: #fff;
    font-weight: 300;
    height:100%;
    display: grid;
    align-items: center;

}
@media (min-width: 768px) {
  .panel .task-input {
      width: 704px;
  }
}
</style>
