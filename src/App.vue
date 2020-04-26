<template>

    <div
        id="app"
        :style="{margin: setMargin}"
    >
        <template v-if="!hasName">
            <div class="fields">
                <label
                    for="name"
                    class="label"
                >Qual o seu<br>nome?</label>
                <input
                    id="name"
                    v-model="name"
                    type="text"
                    placeholder="seu nome"
                    class="input"
                >
                <button
                    class="btn"
                    @click="saveName"
                >
                    Iniciar
                </button>
            </div>
        </template>
        <template v-else>
            <Greeting :name="getName" />
            <Tasks />
        </template>
    </div>
</template>

<script>
import Greeting from './components/Greeting'
import Tasks from './components/Tasks'

export default {
    components: { Greeting, Tasks },
    data () {
        return {
            name: ''
        }
    },
    computed: {
        hasName () {
            return localStorage.getItem('taskUserName') ? true : false
        },
        setMargin () {
            return this.hasName ? '16px' : 0
        },
        getName () {
            return localStorage.getItem('taskUserName')
        }
    },
    methods: {
        saveName () {
            if (this.name) {
                localStorage.setItem('taskUserName', this.name)
                document.location.reload()
            }
        }
    }
}
</script>

<style>
/* Fonts */
@import url("https://fonts.googleapis.com/css?family=Roboto:100,300,400,900");

body {
    margin: 0;
    padding: 0;
}

#app {
    font-family: "Roboto", sans-serif;
    font-size: 18px;
    font-weight: 100;
    text-align: center;
    color: #000;
    display: grid;
    justify-items: center;
    background-color: #fff;
}
.fields {
    display: grid;
    grid-template-columns: 1fr;
    justify-items: center;
    align-items: center;
    background-color: #ff3366;
    width: 100vw;
    height: 100vh;
}
.fields input {
    border: 1px solid #e0e0e0;
    border-radius: 10px;
    height: 48px;
    width: 300px;
    padding: 10px;
    font-size: 20px;
    font-weight: 100;
    box-sizing: border-box;
}

.fields button {
    border: 0;
    width: 300px;
    height: 48px;
    background-color: #fff;
    color: #000;
    font-size: 24px;
    font-family: "Roboto", sans-serif;
    font-weight: 100;
    border-radius: 10px;
    align-self: start;
}
.fields input:focus,
.fields button:focus {
    outline: 0px;
}
.label {
    font-size: 40px;
    font-weight: 100;
    color: #fff;
    align-self: end;
}
</style>
