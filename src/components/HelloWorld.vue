<template>
  <div>
    <v-scroll :onLoadMore="onLoadMore" :dataList="scrollData">
      <ul>
        <li v-for="(item) in listdata" :key="item.name">{{item.name}}</li>
        <li v-for="(item) in downdata" :key="item.name">{{item.name}}</li>
      </ul>
    </v-scroll>
  </div>
</template>
<style lang="less">
  ul li {
    min-height: 100px;
    line-height: 100px;
    text-align: center;
    border: 1px solid red;
  }
</style>
<script>
  import loadmore from "./scroll.vue";
    export default {
        components: {
            'v-scroll': loadmore
        },
        data() {

            return {
                counter: 1, //当前页
                num: 10, // 一页显示多少条
                pageStart: 0, // 开始页数
                pageEnd: 0, // 结束页数
                listdata: [], // 下拉更新数据存放数组
                downdata: [], // 上拉更多的数据存放数组
                scrollData:{
                    noFlag: false //暂无更多数据显示
                }
            }
        },
        mounted: function() {
            this.getList();
        },
        methods: {
            getList() {
                var response = []
                for(let i = 0; i < 60; i++) {
                    response.push({
                        name: i
                    })
                }
                this.listdata = response.slice(0, this.num);
            },

            onLoadMore(done) {
                this.counter++;
                let end = this.pageEnd = this.num * this.counter;
                let i = this.pageStart = this.pageEnd - this.num;

                setTimeout(() => {
                    for(i; i < end; i++) {
                        if(i >= 30) {

                            //走完数据调用方法
                            // this.scrollData.noFlag = true;

                            break;
                        } else {
                            this.downdata.push({
                                name: i + "==="
                            })
                            // more.style.display = 'none'; //隐藏加载条
                        }
                    }
                    done();
                }, 2000);
            }
        }

    }
</script>