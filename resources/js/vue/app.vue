<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 id="title">Todo List</h2>
            <addItemForm v-on:reloadlist="getList()"/>
        </div>
        <listView :items="items" v-on:reloadlist="getList()"/>
    </div>
</template>

<script>
import addItemForm from './addItemForm.vue'
import listView from './listView.vue'

export default ({
    components: {
        addItemForm,
        listView
    },
    data: function () {
        return {
            showP: true,
            items: [],
            learnings: [],
        }
    },
    methods: {
        getList () {
            axios.get('api/items')
           
            .then( response => {
                this.items = response.data
            })
            .catch ( error  => {
                console.log( error )
            })
        }
    },
    created() {
        this.getList();
    }
})
</script>

<style scoped>
.todoListContainer {
    padding-top: 10rem;
    width: 350px;
    margin: auto;
}
.heading {
    background: #e6e6e6;
    padding: 10px;
}
#title {
    text-align: center;
}


</style>
