<template>
    <div class="container">
        <button v-for="(button, key) in buttons" :key="button.id">{{ key }}</button>
        <button>.</button>
        <button v-for="(operator, key) in operators" :key="operator.id">{{ key }}</button>
        <button>=</button>
        <button>C</button>
    </div>
</template>

<script>
    export default {
        name: 'Button',
        props: ['buttons', 'operators'],
    }
</script>