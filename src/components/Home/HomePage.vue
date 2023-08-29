<template>
    <div>
        <button @click="showModal = !showModal">Добавить продукт</button>
        <div class="product">
            <div v-for="{name, price} in products" :key="name">
                <Cart :name="name" :price="price" @delete="onDelete"/>
            </div>
        </div>
        <div class="modal" v-if="!showModal">
            <div class="modalBlock">
                <button @click="closeModal">✖</button>
                <div class="modalItem">
                    <div>Продукт</div>
                    <input v-model="name">
                </div>
                <div class="modalItem">
                    <div>Цена</div>
                    <input v-model="price">
                </div>
                <button @click="add">Добавить</button>
            </div>
        </div>
    </div>
</template>

<script>
    import Cart from "@/components/Cart/Cart";
    import './home.css';

    export default {
        name: "HomePage",
        components: {
            Cart
        },
        data: function () {
            return {
                price: '',
                name: '',
                showModal: true,
                products: [
                    {name:"Печенье Семейка Озби бисквитное Сладяша апельсин в белой глазури 400г", price:"199.99"},
                    {name:"Пельмени Сибирская Коллекция Иркутские 700г", price:"739.99"},
                    {name:"Колбаса Армавирский МК Московская сырокопченая\n" +
                            "400г", price:"499.96"},
                    {name:"Шашлык Французский сад из свинины в маринаде\n" +
                            "1кг", price:"359.99"},
                    {name:"Стейк из грудки индейки Индилайт 525г", price:"309.99"},
                    {name:"Паштет Деликатес Дичь из утиной печени с шампанским 200г", price:"219.99"},
                ],
            };
        },
        mounted() {
            // localStorage.removeItem('products');
            if (localStorage.products) {
                this.products = JSON.parse(localStorage.getItem('products'));
            }
        },
        methods: {
            add: function () {
                this.products.push({name: this.name, price: this.price, textDecoration: this.textDecoration})
                localStorage.setItem('products', JSON.stringify(this.products));
                this.showModal = !this.showModal;
                this.price = "";
                this.name = "";
            },
            closeModal: function () {
                this.showModal = !this.showModal;
            },
            onDelete: function (data) {
                const fromIndex = this.products.findIndex((element) => JSON.stringify(data.name) === JSON.stringify(element.name));
                const item = this.products.splice(fromIndex, 1)[0];
                this.products.splice(this.products.length, 1, item);
                localStorage.setItem('products', JSON.stringify(this.products))
            }
        }

    }
</script>

<style scoped>

</style>