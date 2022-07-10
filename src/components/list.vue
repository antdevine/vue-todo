<template>
    <div>
        <h2>Item:</h2>
        {{listItem}}

        <button @click="$emit('remove', listItemId)">Remove</button>
        <button @click="$emit('complete', listItemId)">Completed</button>
    </div>
</template>

<script>
    export default {
        name: 'List',
        data() {
        return {
            
            }
        },
        mounted() {
         console.log(this.listItem, 'this listItem'); 
        },
        methods: {            
        },
        props: {
            listItem: {
                type: String,
                required: false
            },
            listItemId: {
                type: Number,
                required: false
            }
        }
    };
</script>
