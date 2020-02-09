<template>
    <div>
        <div class="option_list">
            <p v-for="(option, id) in passedOptions" :key="id" :class="{highlight:option == getSelected()}"
                @click="updateSelected(option)" v-html="option">
                {{option}}
            </p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Options',
    props: {
        options: Array,
        selected: undefined,
    },
    methods: {
        updateSelected: function(passedOption) {
            this.selected = passedOption

            // Also make the next button active
            this.$parent.activeNext()
        },
        getSelected: function() {
            return this.selected
        }
    },
    computed: {
        passedOptions: function() {
            return this.options
        }
    }
}
</script>

<style scoped>
    p {
        width: 50%;
        padding: .5rem;
        border: 1px solid #212121;
        margin: .2rem;
        display: inline-block;
        border-radius: 30px;
        padding: .7rem 3.5rem;
        transition: .3s;
    }
    p:hover, .highlight {
        background: #5C6BC0;
        color: #fff;
    }
    .option_list {
        text-align: center;
    }
</style>