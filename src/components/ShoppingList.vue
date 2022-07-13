<template>
    <div class="shopping-list">
        <h1>Shoping list</h1>
        <label>
            <input placeholder="Press enter to add new item" type="text" v-model="newItem" @keyup.enter="addItem(newItem)"/>
            <a class="add-btn btn" href="#" @click="addItem(newItem)">Add item</a>
        </label>
        <div v-if="items.length> 0">
            <ul>
                <li v-for="(item, n) in items" :key="n">
                    {{item}} <a class="remove-btn" href="#" @click="deleteItem(item)">REMOVE</a>
                </li>
            </ul>
            <a class="delete-btn btn" href="#" @click="deleteAllItems()">Delete all</a>
        </div>
    </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue'

type Item = string

export default defineComponent({
    data() {
        return {
            newItem: '',
            items: [] as Item[],
        }
    },
    methods: {
        addItem(item: string): void {
            if(item.trim()) this.items.push(item)
            this.newItem = ""
        },
        deleteItem(item: Item):void {
            this.items = this.items.filter(currentItem => currentItem !== item)
        },
        deleteAllItems():void {
            this.items = []
        }
    }
})
</script>

<style lang="scss" scoped>
h1 {
    text-align: left;
    font-weight: bold;
    color: rgb(42, 42, 42);
}

label {
    width: 100%;
    display: flex;
    justify-content: space-between;
}

input {
    min-width: 80%;
    height: 35px;
    + .btn {
        margin-left: 20px;
    }
}

a {
    text-decoration: none;
}

ul {
    display: block;
    padding: 10px;
    border: solid 1px rgb(113, 113, 113);
    margin: 30px 0px;
    min-height: 30px;
}

li {
    padding-left: 10px;
    display: flex;
    max-width: 90%;
    justify-content: space-between;
    margin: 20px 20px;
}

.shopping-list {
    display: block;
    max-width: 800px;
    margin: 0 auto;
}

.btn {
    padding: 10px 20px;
    font-weight: bold;
    border-radius: 10px;
}

.add-btn {
    background: rgb(96, 96, 96);
    color: white;
}

.remove-btn {
    color: red;
    font-weight: bold;
}

.delete-btn {
    background: rgb(198, 5, 5);
    color: white;
}
</style>