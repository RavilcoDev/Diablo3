<template>
  <!-- Clase CSS que determina el color -->
  <div class="text-center bg-dark h-100 pt-3 d3-icon-item" :class="itemClassColor">

    <div class="d-flex flex-column justify-content-between h-100">
      <!-- Si el item tiene `id`, es que tenemos la información -->
      <!-- Es decir, que tiene un objeto equipado. -->
      <template v-if="item.id">
        <div>
          <div v-if="item" class="item-image">
            <!-- Nombre del objeto -->
            <p class="text-muted">{{ item.name }}</p>
            <!-- Imagen correspondiente al objeto -->
            <img :src="itemUrl" :alt="item.slotName + ' ' + item.name ">
          </div>
        </div>

        <div>
          <!-- No todos los objetos tienen gemas -->
          <!-- Por lo tanto, si el objeto tiene gemas engarzadas -->
          <template v-if="itemHasGems">
            <!-- Puede ser Gema o Joya -->
            <small>{{ gemOrJewel }}:</small>
            <ul class="list-inline pl-0">
              <!-- Un objeto puede tener varias gemas -->
              <li v-for="(gem, index) in item.gems" :key="'gem-'+index" class="list-inline-item">
                <!-- Componente gema -->
                <item-detail-gem :gem="gem"/>
              </li>
            </ul>
          </template>
        </div>
      </template>
      <!-- En caso de que no tenga el objeto equipado -->
      <p v-else>
        <!-- Mostramos el nombre del slot y dejamos el contenido vacío -->
        <span class="text-dark bg-primary"> {{item.slotName}}</span>
      </p>
    </div>

  </div>
</template>

<script>

import ItemDetailGem from './ItemDetailGem.vue'
export default {
  name: 'ItemDetail',
  components: { ItemDetailGem },
  props: {
    item: {
      type: Object || undefined,
      required: true
    }
  },
  computed: {
    itemUrl () {
      const host = 'http://media.blizzard.com/d3/icons/items/large/'
      return `${host}${this.item.icon}.png`
    },
    itemHasGems () {
      return Object.prototype.hasOwnProperty.call(this.item, 'gems')
    },
    gemOrJewel () {
      return this.item.gems[0].isGem ? 'Gems' : 'Jewel'
    },
    itemClassColor () {
      if (Object.prototype.hasOwnProperty.call(this.item, 'displayColor')) {
        return `item-${this.item.displayColor}`
      }
      return 'item-none'
    }
  }
}
</script>

<style lang="stylus">
  .d3-icon-item
    min-height 100px
    border-top-style solid
    border-top-width 4px

    &.item-none
      border-color transparent

    &.item-green
      border-color #8bc34a

    &.item-orange
      border-color #ff9800

    &.item-yellow
      border-color #ffeb3b

    &.item-blue
      border-color #03a9f4

    &.item-white
      border-color #a0aab5
</style>
