<template>
    <div class="cart">
        <div>
            <div :style="!text ? 'text-decoration: line-through;' : 'text-decoration: none;'" class="cartItemLeft">
                {{name}}
            </div>
            <div :style="!text ? 'text-decoration: line-through;' : 'text-decoration: none;'"
                 class="cartItemRight cartPrice">{{price}} ₽
            </div>
        </div>
        <img class="cartDelete" width="18" height="18" src="@/assets/delete.png" @click="showTextDecoration"
             alt="Удалить">
    </div>
</template>

<script>
    import './cart.css'

    export default {
        // eslint-disable-next-line vue/multi-word-component-names
        name: "Cart",
        props: ['name', 'price'],
        data: function () {
            return {
                text: true,
            };
        },
        methods: {
            showTextDecoration: function () {
                // console.log(this.textDecoration)
                this.text = !this.text;
                this.$emit('delete', {
                    name: this.name,
                    price: this.price,
                })
            }
        }
    }
</script>

<style scoped>

</style>