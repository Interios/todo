<template>
    <div class="container">
        <input type="text" @keyup.enter="handleAddClick" v-model="field">
        <div class='todo'>
            <transition-group name="list" tag="ul">
                <li class="todo-item" v-for="(item, index) in list" :key="index" v-ripple>
                    <p>{{ item }}</p>
                    <button @click="handleDeleteClick(index)">Delete</button>
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
            this.list.push(
                e.target.value,
            );
            this.field = '';
        },
        handleDeleteClick(index) {
            this.list.splice(index, 1);
        }
    }
}
</script>

<style>
    .todo ul {
        list-style: none;
        width: 500px;
        margin: auto;
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
        box-shadow: -1px 0px 14px 3px rgba(0,0,0,0.35);
        /* transition: all 1s; */
    }
    .todo-item p {
        margin: 0;
        padding-top: 5px;
    }
    .todo-item button {
        background-color: #23d160;
        border-color: transparent;
        color: #fff;
        border-radius: 4px;
        padding: 5px 10px;
    }

    .list-enter-active,
    .list-move {
        transition: 500ms cubic-bezier(0.59, 0.12, 0.34, 0.95);
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
        transition: .5s ease;
    }

    .list-leave-to {
        opacity: 0;
        transform: scaleY(0);
        transform-origin: center top;
    }
</style>