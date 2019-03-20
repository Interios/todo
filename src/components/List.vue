<template>
    <div class="toDo-wrap">
        <h2>{{ title }}</h2>
        <div class='toDo-title'>
            <input type="text" @keyup.enter="handleAddClick" v-model="field">
            <button class="btn-delete" @click="$emit('remove')">Delete ToDo list</button>
        </div>
        <div class='todo'>
            <transition-group name="list" tag="ul">
                <li class="todo-item" v-for="(item, i) in list" :key="i" v-ripple >
                    <button class="btn-edit" @click="item.like++">Like {{ item.like }}</button>
                    <div class='todo-item__context'>
                        <p v-if="!item.edit">{{ item.name }}</p>
                        <input v-if="item.edit" v-model='item.name' type="text">
                    </div>
                    <button class="btn-edit" @click="handleEditClick(i)">Edit</button>
                    <button class="btn-delete" @click="handleDeleteClick(i)">Delete</button>
                </li>
            </transition-group>
        </div>
    </div>
</template>

<script>
export default {
    name: 'ToDoList',
    data: () => ({
        list: [],
        field: ''
    }),
    props: {
        title: String
    },
    // computed: {
    //     setKeys: function() {
    //         return this.list.map( (el, index) => {
    //             return {
    //                 name: el,
    //                 key: index
    //             }
    //         } )
    //     }
    // },
    methods: {
        handleAddClick(e) {
            if(!e.target.value) return;
            this.list.push({
                name: e.target.value,
                like: 0,
                edit: false
            });
            this.field = '';
        },
        handleDeleteClick(index) {
            this.list.splice(index, 1);
        },
        handleEditClick(index) {
            this.list[index].edit = !this.list[index].edit;
        }
    }
}
</script>

<style>
    .toDo-title {
        display: flex;
        justify-content: space-between;
    }
    .toDo-wrap {
        box-shadow: -1px 0px 14px 3px rgba(0,0,0,0.35);
        padding: 20px;
        margin-top: 40px;
    }
    .todo ul {
        list-style: none;
        position: relative;
    }
    .todo-item {
        margin: 20px 0;
        position: relative;
        overflow: hidden;
        cursor: pointer;
        padding: 10px;
        display: flex;
        justify-content: space-between;
        width: 100%;
        box-shadow: -1px 0px 14px 3px rgba(0,0,0,0.35);
        /* transition: all 1s; */
    }
    .todo-item p {
        margin: 0;
        padding-top: 5px;
    }
    .todo-item__context {
        text-align: left;
        flex: 1;
    }
    .btn-edit {
        background-color: #237fdc;
        border-color: transparent;
        color: #fff;
        border-radius: 4px;
        padding: 5px;
        margin-right: 5px;
    }
    .btn-delete {
        background-color: #23d160;
        border-color: transparent;
        color: #fff;
        border-radius: 4px;
        padding: 5px 10px;
    }

    .list-enter-active,
    .list-leave-active,
    .list-move {
        transition: 500ms cubic-bezier(0.59, 0.12, 0.34, 0.95);
        transition-property: opacity, transform;
    }
    .list-enter {
        opacity: 0;
        transform: translateX(50px) scaleY(0.5);
    }

    .list-enter-to {
        opacity: 1;
        transform: translateX(0) scaleY(1);
    }

    .list-leave-active {
        position: absolute;
    }

    .list-leave-to {
        opacity: 0;
        transform: scaleY(0);
        transform-origin: center top;
    }
</style>