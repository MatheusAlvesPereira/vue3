<template>
    <h1 class="title">Drag And Drop Elements</h1>

    <div class="dragAndDrop"
    @drop="onDrop($event, 1)"
    @dragover.prevent
    @dragenter.prevent
    >
        <div v-for="item in getList(1)" 
        :key="item.id" class="item" 
        draggable="true" 
        @dragstart="startDrag($event, item)"
        >
            {{ item.title }}
        </div>
    </div>

    <div class="dragAndDrop"
    @drop="onDrop($event, 2)"
    @dragover.prevent
    @dragenter.prevent
    >
        <div v-for="item in getList(2)" 
        :key="item.id" class="item" 
        draggable="true" 
        @dragstart="startDrag($event, item)">
            {{ item.title }}
        </div>
    </div>
</template>

<script setup>
    import { ref } from 'vue'

    const listItems = ref([
        { id: 1, title: 'Item 1', list: 1},
        { id: 2, title: 'Item 2', list: 1},
        { id: 3, title: 'Item 3', list: 2},
    ])

    const getList = (list) => {
        return listItems.value.filter(item => item.list == list)
    }

    const startDrag = (event, item) => {
        console.log('startDrag', item)
        event.dataTransfer.dropEffect = "move";
        event.dataTransfer.effectAllowed = "move";
        event.dataTransfer.setData("itemID", item.id);
    }

    const onDrop = (event, list) => {
        console.log('onDrop', list)
        const itemID = event.dataTransfer.getData("itemID");
        const item = listItems.value.find((item) => item.id == itemID)
        item.list = list
    }
</script>

<style>

.title{
    padding-top: 100px;
    text-align: center;
}

.dragAndDrop {
    width: 50%;
    margin: 50px auto;
    background-color: blanchedalmond;
    padding: 10px;
    min-height: 10px;
}

.item{
    background-color: aquamarine;
    padding: 5px;
    margin-bottom: 10px;
}

.dragAndDrop:nth-last-of-type(1){
    margin-bottom: 0;
}

</style>