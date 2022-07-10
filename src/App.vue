<template>
  <div>

    <header>
    <h1>This is the List</h1>
  </header>

  <main>
    <List 
    v-for="item in this.listItems" 
    :key="item.id" 
    :listItem="item.item" 
    :listItemId="item.id"
    @remove="removeItem" 
    @complete="completedItem" />

    <input type="text" v-model="newItem" placeholder="add item" />
    <input type="button" value="Add item" @click="addItem" />

    <p v-if="message">{{this.message}}</p>

    <div v-if="this.completedListItems.length">
      <CompletedList 
      v-for="item in this.completedListItems" :key="item.id" :completedListItem="item.item" :completedListItemId="item.id" />
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
        newItem: '',
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
        addItem() {
          if (this.newItem.length) {

            const lastItemId = this.listItems.length ? this.listItems[this.listItems.length - 1] : 0;
            const newItemId = this.listItems.length ? Number(lastItemId.id) + 1 : 1;

            this.listItems.push({"id": newItemId, "item": this.newItem});

            this.newItem = '';
          }
        },
        completedItem(id) {
          this.message = `You completed item ${id}`;

          const completedList = this.listItems.filter(items => {
            return items.id === id;
          });
          this.completedListItems.push({"id": completedList[0].id, "item": completedList[0].item});

          const origianlList = this.listItems.filter(items => {
            return items.id !== id;
          });

          this.listItems = origianlList;
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
