<template>
    <div>
      <h1>Boutique</h1>
      <div class="list-container">
        <ItemsList />
      </div>
      <div class="list-container">
        <BasketList />
      </div>
    </div>
  </template>
  
  <script>
  import ItemsList from "@/components/ItemsList.vue";
  import BasketList from "@/components/BasketList.vue";
  
  export default {
    components: {
      ItemsList,
      BasketList,
    },
  };
  </script>
  
  <style>
  .list-container {
    display: inline-block;
    width: 50%;
    padding: 10px;
    box-sizing: border-box;
  }
  </style>