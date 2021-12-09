<template>
    <div>
        <h3>Movimientos</h3>
        <ul>
            <li v-for="(mov, index) in data" :key="index">{{ mov.move.name }}</li>
        </ul>
    </div>
</template>

<script>
export default {
    props: ['data'],
    // setup(props) {
        
    //     const usingProps = ()=> {
    //         console.log(props.data)
    //     }

    // }
}
</script>
