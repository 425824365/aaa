
<template>
<div id="chatContainer">
<ul class="infinite-list " v-infinite-scroll="load" style="
height: 500px;
    padding: 0;
    margin: 0;">
      <li v-for="(i,index) in count" :key="index" class="infinite-list-item">{{ i }}</li>

  </ul>
</div>
  
</template>

<script>
  export default {
    data () {
      return {
        count: 0
      }
    },
        updated() {
		this.scrollToBottom(); //每次页面渲染完之后滚动条在最底部
	},
    methods: {
      load () {
        console.log(222)
        this.count += 2
      },
           	scrollToBottom: function() {
			this.$nextTick(() => {
				//Vue 在更新 DOM 时是异步执行的，为了在数据变化之后等待 Vue 完成更新 DOM，可以在数据变化之后立即使用 Vue.nextTick(callback)。这样回调函数将在 DOM 更新完成后被调用。
        var container = document.getElementById('chatContainer')
        container.scrollTop = container.scrollHeight;
			});
		},
    }
  }
</script>
<style lang="scss" scoped>
#chatContainer{

background: greenyellow;
overflow: hidden;
overflow-y: auto;
}
</style>