<template>
  <div>

    <header>
    <h1>This is the List</h1>
  </header>

  <main>
    <List v-for="item in this.listItems" :key="item.id" :listItem="item.item" :listItemId="item.id" @remove="removeItem" @completed="completedItem" />

    <input v-model="addItem" placeholder="add item" />
    <input type="button" value="Add item" @click="addedItem" />

    <p v-if="message">{{this.message}}</p>

    <div v-if="this.completedListItems.length">
      <CompletedList v-for="item in this.completedListItems" :key="item.id" :completedListItem="item.item" :completedListItemId="item.id" />
    </div>
  </main>
  </div>
</template>

<script>
  import List from './components/list.vue';
  import CompletedList from './components/completedList.vue';

  export default {
    components: {
    List,
    CompletedList
},
    data() {
      return {
        listItems: [
            {
                "id": 1,
                "item": "Milk"
            },
            {
                "id": 2,
                "item": "Bread"
            },
            {
                "id": 3,
                "item": "Cheese"
            }
        ],
        completedListItems: [],
        message: '',
        itemAdded: false,
        addItem: '',
        completedItem: '',
      }
    },
    methods: {
      removeItem(id) {
                this.message = '';

                if (this.listItems.length === 1) {
                  this.message = 'You have no items in your list';
                } else {
                  this.message = `you removed item ${id}`;
                }

                const edittedList = this.listItems.filter(items => {
                  return items.id !== id;
                });

                this.listItems = edittedList;
            },
        addedItem() {
          if (this.addItem.length) {
            console.log(this.addItem, 'item added addItem');
            if(this.listItems.length) {
                // Get the last item id in the array
                var lastItemId = this.listItems[this.listItems.length - 1];
                console.log(lastItemId.id, 'lastItemId');
                let newItemId = Number(lastItemId.id) + 1;

                this.listItems.push({"id": newItemId, "item": this.addItem});
            }
          }
        },
        completedItem(id) {
            this.message = `You completed item ${id}`;

            const completedList = this.listItems.filter(items => {
              return items.id === id;
            });

                // Get the last item id in the array
                var lastCompletedItemId = this.completedListItems[this.completedListItems.length - 1];
                console.log(completedLastItemId.id, 'completedLastItemId');
                let newCompletedItemId = Number(completedLastItemId.id) < 1 ? 1 : Number(completedLastItemId.id) + 1;

                this.completedListItems = completedList;
                this.completedListItems.push({"id": newCompletedItemId, "item": this.completedItem});
        },
    },
    mounted() {
      console.log('the component is now mounted.', this.listItems);
    }
  };
</script>

<style>
  @import './assets/base.css';
</style>
