<template>
    <button @click="click" :disabled="isPrevButtonDisabled" class="mybtn">{{ text }}</button>
</template>

<script>
export default {
    props: {
        isDisabled: {
            type: Boolean,
            default: false,
        },
        text: {
            type: String,
            required: true
        }
    },
    methods: {
        click() {
            this.$emit("click");
        }
    },
    computed: {

    }
}
</script>

<style lang="scss">
.mybtn {
    padding: 0px;
    font-size: 16px;
    color: #ffffff;
    border: none;
    border-radius: 5px;
    background-color: transparent;
}
</style>