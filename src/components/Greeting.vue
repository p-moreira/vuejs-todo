<template>
    <div class="panel greeting">
        <img
            :src="require(`../assets/${greeting.img}.svg`)"
            :alt="greeting.img"
        >
        <h1>
            <span>{{ greeting.msg }},</span>
            <span>{{ name }}!</span>
        </h1>
    </div>
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            default: ''
        }
    },
    computed: {
        greeting () {
            let hour = new Date().getHours()
            if (hour < 12) {
                return { msg: 'Bom dia', img: 'sol' }
            } else if (hour < 18) {
                return { msg: 'Boa tarde', img: 'sol' }
            } else {
                return { msg: 'Boa noite', img: 'lua' }
            }
        }
    }
}
</script>

<style scoped>
.panel {
    width: 100%;
}
h1 {
    font-size: 40px;
    font-weight: 100;
}
.greeting span {
    display: block;
}
</style>
