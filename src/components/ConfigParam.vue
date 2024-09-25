<script>
export default {
    data() {
        return {
            status: null,
            items: null
        }
    },

    methods: {
        isOpen() {
            this.setItems("Codigo=1;Nome=Test 1;Data=01/01/2024")
            this.status = "open"
        },

        isClosed() {
            this.status = "closed"
            const value = this.getItems()
            console.log('value', value)
        },

        setItems(value) {
            console.log('value', value)
            var itemsAux = []
            const valueList = value.split(";")
            valueList.forEach(valueItem => {
                const valueAux = valueItem.split("=")
                const itemAux = { code: valueAux[0], value: valueAux[1] }
                itemsAux = [...itemsAux, itemAux]
            });
            this.items = itemsAux
        },

        getItems() {
            var value = ""
            this.items?.forEach(item => {
                value += (value ? ";" : "") + `${item.code}=${item.value}`
            });
            return value
        }

    },

    created(){

    },

    mounted(){
        this.isOpen()
    }
}
</script>

<template>
    <div>
        <button v-if="status == 'closed'" v-on:click="isOpen" >open</button>
        <button v-if="status == 'open'" v-on:click="isClosed" >closed</button>
        <div v-if="status == 'open'">
            <h1>Hello World</h1>

            <div v-if="items">
                <div v-for="item in items" :key="item">
                    <input type="text" placeholder="Codigo" v-model="item.code"/>                
                    <input type="text" placeholder="Valor" v-model="item.value"/>                
                </div>
            </div>
        </div>
    </div>
</template>