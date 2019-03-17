<template>
  <footer class="footer">
      <span class="todo-count"><strong>{{count}}</strong> 가지</span>
      <ul class="filters">
        <li v-for="(filterType, idx) in filters" :key="idx">
          <a href="javascript:;"
            :class="{selected: selectedIdx === idx}"
            @click="filteron(filterType,idx)">{{filterType}}</a>
        </li>
      </ul>
  </footer>
</template>

<script>
export default {
  props: {
    count: {type:Number, default:0}
  },
  data(){
    return {
      selectedIdx:0,
      filters: ['모두','미숙','능숙']
    }
  },
  methods: {
    filteron(type,idx){
      this.selectedIdx = idx
      this.$emit("setFilterType",type)
    }
  }
}
</script>

<style scoped>
.footer {margin-top:30px;}
.filters {display:inline-block;}
li {list-style:none; display:inline-block; margin:0 10px;}
a {text-decoration:none; color:#666;}
.selected {color:#000; border:2px solid #000; border-radius:5px; padding:5px;}
</style>