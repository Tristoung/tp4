<template>
    <div>
      <h1>Les virus</h1>
      <hr />
      <CheckedList
        :data="filterItems"
        :fields="['name', 'price', 'promotion']"
        item-check
        :item-button="{ show: true, text: 'Ajouter au panier' }"
        :list-button="{ show: true, text: 'Ajouter au panier (tous)' }"
        :item-amount="true"
        :checked="checked"
        @checked-changed="changeSelection($event)"
        @item-button-clicked="addToCart($event)"
        @list-button-clicked="addToCartAll"
      ></CheckedList>
    </div>
  </template>
  
  <script>
  import { mapState, mapActions } from 'vuex';
  import CheckedList from "@/components/CheckedList";
  
  export default {
    name: 'ItemsList',
    components: { CheckedList },
    data: () => ({
      selected: [],
    }),
    computed: {
      ...mapState('shop', ['items', 'shopUser']),
      checked() {
        let tab = [];
        this.filterItems.forEach(item => {
          let idx = this.items.findIndex(el => el == item);
          if (this.selected.includes(idx)) {
            tab.push(true);
          } else {
            tab.push(false);
          }
        });
        return tab;
      },
      filterItems() {
        let list = this.items;
        return list;
      },
    },
    methods: {
      ...mapActions('shop', ['addToCart', 'addToCartAll']),
      changeSelection(idx) {
        let item = this.filterItems[idx];
        let i = this.items.findIndex(el => el == item);
        let j = this.selected.findIndex(el => el === i);
        if (j !== -1) {
          this.selected.splice(j, 1);
        } else {
          this.selected.push(i);
        }
      },
      addToCart(idx) {
        let item = this.filterItems[idx];
        let quantity = item.amount || 1;
        this.addToCart({ item, quantity });
      },
      addToCartAll() {
        let itemsWithQuantities = this.selected.map(idx => {
          let item = this.items[idx];
          let quantity = item.amount || 1;
          return { item, quantity };
        });
  
        this.addToCartAll({ items: itemsWithQuantities });
        this.selected = [];
      },
    },
  };
  </script>
  