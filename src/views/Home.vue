<template>
        
    <div  >
        <virtual-list
        id="chatContainer"
            style="height: 360px; overflow-y: auto;"
            :data-key="'id'"
            :data-sources="items"
            :data-component="itemComponent"
        />
    </div>
</template>

<script>
    import virtualList from "vue-virtual-scroll-list";
    import Item from "./Item";
    export default {
        components: { "virtual-list": virtualList },
        name: "HelloWorld",
        props: {
            msg: String,
        },
        data() {
            return {
                itemComponent: Item,
                items: [],
            };
        },
        watch:{
          items:{
            handler(v){
              this.scrollToBottom()
            }
          }
        },
        methods: {
            dataSource() {
                for (let i = 1; i <= 10000; i++) {
                    setTimeout(()=>{
this.items.push({
                        id: i,
                        name: i + "模拟字段",
                    });
                    },500)
                }
            },
                   	scrollToBottom: function() {
			this.$nextTick(() => {
				//Vue 在更新 DOM 时是异步执行的，为了在数据变化之后等待 Vue 完成更新 DOM，可以在数据变化之后立即使用 Vue.nextTick(callback)。这样回调函数将在 DOM 更新完成后被调用。
         var container = document.getElementById('chatContainer')
        container.scrollTop = container.scrollHeight;
			});
		},
        },
        mounted() {
              this.dataSource();
        },
    };
</script>
