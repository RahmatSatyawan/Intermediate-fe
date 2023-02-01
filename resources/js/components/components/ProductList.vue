<template>
    <table>
        <tr>
            <th>Name</th>
            <th>Description</th>
            <th>Stock</th>
            <th>Price</th>
            <th>Action</th>
        </tr>

        <tr v-for="(item, index) in listProduct" :key="index">
            <td>{{ item.title }}</td>
            <td>{{ item.desc }}</td>
            <td>{{ item.qty }}</td>
            <td>Rp. {{ item.price }}</td>
            <td>
                <button-atom
                    text="Cart"
                    color="blue"
                    :disabled="item.qty == 0"
                    @emitClick="buttonClick(index)"

                ></button-atom>
            </td>
        </tr>
    </table>
</template>

<script>
export default {
    // data: {},
    props: {
        listProduct: {
            type: Array,
            default: () => {
                return [];
            },
        },
        show: {
            type: String,
            default: "show",
        },
        // isDisabled,
    },
    methods: {
        buttonClick(index) {
            this.$emit("emitClick", index);
        },
    },
};
</script>
