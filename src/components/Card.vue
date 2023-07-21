<template>
    <div class="container" :style="{
        width: width,
        height: height,
        backgroundColor: backgroundColor
    }" :class="classCard">
        <slot name="header" />
        <slot name="content" />
        <slot name="footer" />
    </div>
</template>

<script>
export default {
    props: {
        width: {
            type: [String, Number],
            default: "auto",
        },
        height: {
            type: [String, Number],
            default: "",
        },
        backgroundColor: {
            type: [String],
            default: 'white'
        },
        fadeIn: {
            type: Boolean,
            default: false
        },
        rounded: {
            type: Boolean,
            default: false
        }
    },
    computed: {
        classCard() {
            let myClass = {
                "card__animated": this.fadeIn,
                "card__rounded": this.rounded
            }
            return myClass
        },
    }
}
</script>

<style lang="scss">
.card {
    &__rounded {
        border-radius: 20px;
    }

    &__animated {
        transition: transform .4s;

        &:hover {
            transform: scale(1.02);
        }
    }
}
</style>