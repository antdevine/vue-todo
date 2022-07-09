<template>
    <div>
        <h2>Completed Item:</h2>
        {{completedListItem}}
    </div>
</template>

<script>
    export default {
        name: 'CompletedList',
        data() {
        return {
            
            }
        },
        mounted() {
         console.log(this.completedListItem, 'this completedListItem'); 
        },
        methods: {            
        },
        props: {
            completedListItem: {
                type: String,
                required: false
            },
            completedListItemId: {
                type: Number,
                required: false
            }
        }
    };
</script>
