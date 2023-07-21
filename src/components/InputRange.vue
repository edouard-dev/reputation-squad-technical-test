<template>
    <div class="row-slider__col">
        <div class="row-slider__col__line" v-if="label">
            <p class="row-slider__col__line__text">{{ label }}</p>
            <p class="row-slider__col__line__text__temp">{{ value }}{{ unit }}</p>
        </div>
        <input v-model="modelValue" type="range" :min="min" :max="max" class="row-slider__input">
    </div>
</template>

<script>
export default {
    props: {
        min: {
            type: String,
            required: true
        },
        max: {
            type: String,
            required: true
        },
        value: {
            required: true
        },
        label: {
            type: String,
            required: false
        },
        unit: {
            type: String,
            required: false
        }
    },
    computed: {
        modelValue: {
            get() {
                return this.value;
            },
            set(newValue) {
                this.$emit("change", newValue);
            },
        },
    }
}
</script>

<style lang="scss">
.row-slider {
    display: flex;
    justify-content: space-around;

    &__input {
        max-width: 140px !important;
        padding-left: 20px !important;
        padding-right: 20px !important;
        border-radius: 110px !important;
        background: #FFFFFF66 !important;
    }

    &__col {
        display: flex;
        flex-direction: column;

        &__line {
            display: flex;
            justify-content: space-between;

            &__text {
                color: white;

                &__temp {
                    color: #5887FF;
                }
            }
        }
    }
}
</style>