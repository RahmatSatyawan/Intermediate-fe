<template>
    <div class="container">
        <h1>Semua Produk</h1>
        <product-list
            :listProduct="listProduct"
            @emitClick="addCartClick"
        ></product-list>
        <h1>Keranjang Belanja</h1>
        <cart-list
            :listCart="listCart"
            :totalCart="totalCart"
            @emitClick="removeCartClick"
            @emitClick2="removeAllClick"
        >
        </cart-list>

        <button-atom
            class="btn btn-primary"
            text="Checkout"
            color="blue"
            :disabled="listCart.length == 0"
            @emitClick="checkoutClick"
        ></button-atom>
        <button class="btn btn-primary">Button</button>
    </div>
</template>

<script>
// import { filter } from 'vue/types/umd';
// import CartList from "./components/CartList.vue";
export default {
    // components: { CartList },
    data() {
        return {
            listProduct: [
                {
                    title: "Indomie Goreng Rendang",
                    desc: "Masakan instan terenak di dunia",
                    qty: 10,
                    price: 3900,
                },
                {
                    title: "Mie Gelas Rendang",
                    desc: "Mie instan khusus anak kosan",
                    qty: 3,
                    price: 1500,
                },
                {
                    title: "Bakmi Mewah",
                    desc: "Kalau anak kosan jangan macam2 deh",
                    qty: 80,
                    price: 10000,
                },
            ],
            listCart: [
                // {
                //     title: "Bakmi Mewah",
                //     desc: "Kalau anak kosan jangan macam2 deh",
                //     qty: 20,
                //     price: 10000,
                // },
                // {
                //     title: "Indomie Goreng Rendang",
                //     desc: "Masakan instan terenak di dunia",
                //     qty: 10,
                //     price: 3900,
                // },
                // {
                //     title: "Mie Gelas Rendang",
                //     desc: "Mie instan khusus anak kosan",
                //     qty: 10,
                //     price: 1500,
                // },
            ],
            totalCart: 0,
            // isDisable: false,
            // newCartDefault: {
            //     title: null,
            //     qty: 0,
            //     price: 0,
            // },
        };
    },
    methods: {
        checkoutClick() {
            this.totalCart = 0;
            this.totalCart = this.listCart.reduce((acc, item) => {
                return acc + item.qty * item.price;
            }, 0);

            console.log("Checkout clicked.");
            alert(`Checkout clicked.

            Total belanja: ${this.totalCart}`);
        },

        addCartClick(index) {
            let newCart = {
                title: null,
                qty: 0,
                price: 0,
            };

            newCart = {
                title: this.listProduct[index].title,
                qty: 1,
                price: this.listProduct[index].price,
            };

            if (
                this.listCart.filter((e) => e.title == newCart.title).length > 0
            ) {
                for (let i = 0; i < this.listCart.length; i++) {
                    alert("iterasi");
                    if (
                        newCart.title == this.listCart[i].title &&
                        this.listProduct[index].qty > 0
                    ) {
                        return (
                            alert("iterasi 2"),
                            (this.listCart[i].qty += 1),
                            (this.listProduct[index].qty -= 1)
                        );
                    }
                    if (
                        newCart.title == this.listCart[i].title &&
                        this.listProduct[index].qty == 0
                    ) {
                        return (
                            alert("iterasi 3"),
                            (this.listProduct[index].qty = 0)
                            // (this.isDisabled = true)
                        );
                    }
                }
            } else {
                this.listCart.push(newCart), (this.listProduct[index].qty -= 1);
                alert("nooooo");
            }
        },

        removeCartClick(index) {
            if (this.listCart[index].qty > 1) {
                for (let i = 0; i < this.listProduct.length; i++) {
                    if (
                        this.listCart[index].title == this.listProduct[i].title
                    ) {
                        return (
                            (this.listCart[index].qty -= 1),
                            (this.listProduct[i].qty += 1)
                        );
                    }
                }
            } else {
                for (let i = 0; i < this.listProduct.length; i++) {
                    if (
                        this.listCart[index].title == this.listProduct[i].title
                    ) {
                        return (
                            this.listCart.splice(index, 1),
                            (this.listProduct[i].qty += 1)
                        );
                    }
                }
            }
        },

        removeAllClick(index) {
            this.listCart.splice(index, 1);
            console.log("removeAll clicked.");
            alert(`RemoveAll clicked${index}
            Total belanja: ${this.listCart.length}`);
        },
    },
    mounted() {
        console.log("Component todo mounted.");
    },
};
</script>
