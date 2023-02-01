<template>
    <table>
        <tr>
            <th>Name</th>
            <th>Quantity</th>
            <th>Price</th>
            <th>Action</th>
        </tr>

        <tr v-for="(item, index) in listCart" :key="index">
            <td>{{ item.title }}</td>
            <td>{{ item.qty }}</td>
            <td>Rp. {{ item.price }}</td>
            <td>
                <button-atom
                    text="Delete One"
                    color="blue"
                    @emitClick="buttonClick(index)"
                ></button-atom>
                <button-atom
                    text="Delete All"
                    color="blue"
                    @emitClick="buttonClick2(index)"
                ></button-atom>
            </td>
        </tr>
        <tr>
            <td colspan="3">Total</td>
            <td>Rp. {{ totalCart }}</td>
        </tr>
    </table>
</template>

<script>
export default {
    // data: {},
    props: {
        listCart: {
            type: Array,
            default: () => {
                return [];
            },
        },
        totalCart: {
            type: Number,
            default: 0,
        },
    },
    methods: {
        buttonClick(index) {
            this.$emit("emitClick", index);
        },
        buttonClick2(index) {
            this.$emit("emitClick2", index);
        },
    },
};
</script>
