<template>
  <div id="app">
    <div class="table">
      <div v-for="(item, index) in namesJSONCopy" 
        :key="item['G']" 
        class="table-inner" 
        :ref="'item__' + index">
        <div class="table-inner__item">
          <div class="table-inner__item__heading-wrap" @click="closeTab(index)">
            <p class="table-inner__item__heading">
              {{ item['G'] }} 
            </p>
            <i class="arrow down" :ref="'arrow__' + index"></i>
          </div>
          <p v-for="(itemOne, index) in item['B']" :key="index" class="table-inner__item__main">
            {{ itemOne['N'] }} 
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import namesJSON from '../names.json';
  import dataJSON from '../data.json';

  export default {
    name: 'AppVue',
    data() {
      return {
        items: [],
        emptyItem: null,
        dataJSONCopy: structuredClone(dataJSON),
        namesJSONCopy: structuredClone(namesJSON)
      }
    },
    components: {

    },
    methods: {
      closeTab(index) {
        let arrTemp = this.$refs['item__' + index][0].children[0].children;
        for (let i = 0; i < arrTemp.length; i++) {
          if (arrTemp[i].className === 'table-inner__item__main') {
            if (arrTemp[i].style.display === 'none') {
              arrTemp[i].style.display = 'flex';
              this.$refs['arrow__' + index][0].className = 'arrow down';
            } else {
              arrTemp[i].style.display = 'none';
              this.$refs['arrow__' + index][0].className = 'arrow up';
            }
          }
        }
      },
      async loadData() {
   
      }
    },
    mounted() {
      this.loadData()
    },
  }
</script>


<style lang="scss">
  .table {
    * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
    }

    display: flex;
    max-width: 70%;
    flex-direction: column;

    &-inner {
      display: flex;
      flex-wrap: wrap;

      &__item {
        display: flex;
        flex-direction: column;
        margin: 5px;
        border: 1px solid #00000059;
        border-radius: 5px;
        width: 500px;
        position: relative;

        p {
          padding: 5px;
        }

        &__heading {
          cursor: pointer;
          background-color: rgb(0 67 255 / 25%);
        }
      }
    }
  }

  .arrow {
    border: solid black;
    border-width: 0 3px 3px 0;
    display: inline-block;
    padding: 3px;
    position: absolute;
    top: 10px;
    right: 10px;
  }

  .up {
    transform: rotate(-135deg);
    -webkit-transform: rotate(-135deg);
  }

  .down {
    transform: rotate(45deg);
    -webkit-transform: rotate(45deg);
  }
</style>