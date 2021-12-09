<template>
    <div>
        <h3>Habilidades</h3>
        <ul>
            <li v-for="(ability, index) in data" :key="index">{{ ability.ability.name }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['data']
}
</script>
