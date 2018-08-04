<template>
    <div class="calculator">
        <button class="calculator__button" 
                v-for="(button, key) in buttons" 
                :key="button.id"
                @click="setNum(button)">{{ button }}
        </button>
        <button class="calculator__button" @click="setNum('.')">.</button>
        <button class="calculator__button" 
                v-for="(operator, key) in operators" 
                :key="operator.id" 
                @click="setOperator(operator)">{{ operator }}</button>
        <button class="calculator__button" @click="doMath">=</button>
        <button class="calculator__button" @click="clear">C</button>
    </div>
</template>

<script>
    export default {
        name: 'Button',
        props: ['buttons', 'operators',],
        methods: {
            setNum(val) {
                this.$emit('setNum', val);
            },

            setOperator(oper) {
                this.$emit('setOperator', oper);
            },

            doMath() {
                this.$emit('doMath');
            },

            clear() {
                this.$emit('clear');
            }
        }
    }
</script>

<style lang="scss">
    .calculator {
        display: flex;
        flex-wrap: wrap;
        margin: 3rem auto;
        max-width: 28rem;

        &__button {
            border: none;
            border-radius: 50%;
            color: white;
            cursor: pointer;
            display: flex;
            font-family: 'Avenir', Helvetica, sans-serif;
            font-size: 2rem;
            height: 5rem;
            justify-content: center;
            margin: 1rem;
            transition: color 0.3s ease;
            width: 5rem;
            position: relative;
            z-index: 1;

            &::before,
            &::after {
                border-radius: inherit;
                content: '';
                height: 100%;
                left: 0;
                position: absolute;
                top: 0;
                transition: box-shadow 0.3s ease, transform 0.3s ease;
                width: 100%;
                z-index: -1;
            }

            &::before {
                box-shadow: inset 0 0 0 0 red;
            }

            &::after {
                box-shadow: inset 0 0 0 2.5rem red;
            }

            &:hover {
                color: red;
                &::after {
                    box-shadow: inset 0 0 0 0.15rem red;
                    transform: scale3d(1.2, 1.2, 1.2);
                }
            }

            &:focus {
                outline: none;
            }

            &.active {
                color: red;

                &::before {
                    box-shadow: inset 0 0 0 0.15rem red;
                }

                &::after {
                    box-shadow: inset 0 0 0 0.15rem red;
                    transform: scale3d(1.2, 1.2, 1.2);
                }
            }
        } 
    }
</style>
