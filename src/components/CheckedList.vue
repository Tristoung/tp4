<template>
  <div>
    <p v-for="(item, indexRow) in data" :key="indexRow">
      <input type="checkbox"
             v-if="itemCheck"
             :checked="checked[indexRow]"
             @click="$emit('checked-changed',indexRow)"
      >
      <span v-for="(field, indexCol) in fields" :key="indexCol">
        {{item[field]}}
      </span>
      <input v-if="itemAmount" type="number" v-model="item.amount" placeholder="Amount">
      <button v-if="itemButton && itemButton.show" color="grey" @click="$emit('itemButtonClicked(indexRow)',indexRow)">{{itemButton.text}}</button>
    </p>
    <button v-if="listButton && listButton.show" color="green" @click="$emit('listButtonClicked')">{{listButton.text}}</button>
  </div>
</template>

<script>
export default {
  name: "CheckedList",
  props: {
    data: Array, // les données sources
    fields: Array, // le tableau contenant le nom des champs à afficher
    itemCheck: Boolean, // s'il y a des case à cocher
    checked: Array, // le tableau des cases cochées
    itemButton: Object, // l'objet pour les boutons d'items
    listButton: Object, // l'objet pour le bouton de liste
    itemAmount: Boolean,
  },
  data : () => {
    return {
    }
  },
  methods: {
    itemButtonClicked(indexRow) {
      const amount = this.itemAmount ? this.data[indexRow].amount : null;
      this.$emit('item-button-clicked', { indexRow, amount });
    },
    listButtonClicked() {
      const selectedItemsValues = this.selectedItems.map(indexRow => {
        const amount = this.itemAmount ? this.data[indexRow].amount : null;
        return { indexRow, amount };
      });

      this.$emit('list-button-clicked', selectedItemsValues);

      this.selectedItems = [];
    },
  },
}
</script>