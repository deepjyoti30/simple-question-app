<template>
    <div>
        <button @click="reset">{{ltext}}</button>
        <button @click="next" :disabled="getIsNextDisabled() ? true : false">{{rtext}}</button>
    </div>
</template>

<script>
export default {
    name: 'Button',
    props: {
        ltext: String,
        rtext: String,
    },
    data: function() {
        return {
            isNextDisabled: true
        }
    },
    methods: {
        reset() {
            this.$parent.resetSelected()
        },
        next() {
            this.$parent.moveNext()
        },
        getIsNextDisabled() {
            return this.isNextDisabled
        },
        disableNext() {
            this.isNextDisabled = true
        },
        enableNext() {
            this.isNextDisabled = false
        },
    }
}
</script>

<style scoped>
    div {
        margin: 2rem;
        text-align: center;
    }
    button {
        background: none !important;
        font-size: 12pt;
        margin: 0 .5rem;
        padding: .7rem 4rem;
        text-transform: uppercase;
        font-weight: 600;
        border-radius: 30px;
        outline: none !important;
        border: 2px solid #212121 !important;
        box-shadow: none !important;
    }

    button:hover {
        transition: .2s;
        background: #212121 !important;
        color: #fff;
    }
</style>