<template>
  <div>
    <table>
      <tr>
        <td v-for="(link, index) in titles" :key="index" :style="{paddingRight: '10px'}">
          <button
              @click="$emit('menu-clicked', index)"
              :style="{backgroundColor: link.color}"
              class="nav-button"
          >
            {{link.text}}
          </button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "NavBar",
  props: { titles: Array},
}
</script>

<style scoped>
.nav-button {
  padding: 10px;
}
</style>