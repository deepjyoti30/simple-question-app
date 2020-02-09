<template>
    <div>
        <h1>
            Your score is {{correct}} out of {{total}}
        </h1>
        <h3>
            Thanks for using the app, it's my first app in VueJS.
        </h3>
    </div>
</template>

<script>
export default {
    name: 'Answers',
    props: {
        correct: Number,
        total: Number
    }
}
</script>

<style scoped>
    div {
        text-align: center;
    }
    h1, h3 {
        display: inline-block;
    }
</style>