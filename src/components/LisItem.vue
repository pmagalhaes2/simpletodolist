<template>
    <div>
        <span class="list-item">
          <input type="checkbox" :id="index" class="item-checkbox" v-model="item.checked">
          <label :for="index" :class="item.checked ? 'item-checked' : ''">{{item.label}}</label>
        </span>
        <span v-html="deleteIcon" @click="deleteItem(index)"></span>
    </div>
</template>

<script>

import feather from 'feather-icons';


export default {
  name: 'ListItem',
  props: {
      item: Object,
      index: Number
  },
  computed:{
    deleteIcon(){
    return feather.icons.trash.toSvg({width: 19});
    }
  },
  methods: {
      deleteItem(index) {
          this.$emit('delete-item', index);
        }
    }
}

</script>

<style scoped>

    div{
        width: 100%;
    }

    div, .list-item{
        display: flex;
        align-items: center;
        justify-content: space-between;
        }

    .item-checkbox{
        margin-right: 10px;
    }

    .item-checked{
        text-decoration: line-through;
    }

</style>