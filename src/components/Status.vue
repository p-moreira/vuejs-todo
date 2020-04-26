<template>
    <div class="panel status">
        <h1>Suas Tarefas</h1>
        <div class="completed">
            <div
                class="percent"
                :style="{width: completed + '%'}"
            />
            <div class="percent-number">
                <span>{{ completed }}%</span>
            </div>
        </div>
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
    },
    computed: {
        completed () {
            let total = this.tasks.length
            if (total === 0) {
                return 0
            }
            let completeds = 0
            this.tasks.forEach(task => {
                //console.log(task.completed)
                if (task.completed === true) {
                    completeds++
                }
            })
            //console.log(total, completeds)
            return Math.floor((completeds * 100) / total)
        }
    }
}
</script>

<style scoped>
.panel {
    width: 100%;
}
h1 {
    font-size: 28px;
    font-weight: 100;
    margin: 10px 0;
}
.completed {
    width: 100%;
    height: 40px;
    border: 1px solid #e0e0e0;
    border-radius: 10px;
}
.percent {
    height: 100%;
    background-color: #2ac940;
    border-radius: 10px;
}
.percent-number {
    position: relative;
    top: -70%;
}
@media (min-width: 768px) {
    .panel .status {
        width: 704px;
    }
}
</style>
