<template>
    <div>
        <span>Nombre:</span>
        <input type="text" v-model="name" @keydown.enter="search">
        <button @click="search">Buscar</button>
    </div>
</template>

<script>
import { ref } from "vue"
export default {
    setup(_, {emit}) {
        const name = ref("pikachu")

        const search = ()=> {
            emit("search-pkmn", name.value)
        }

        return { name, search }
    }
}
</script>
