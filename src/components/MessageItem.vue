<!--这个 MessageItem 组件用于显示用户消息，展示了用户头像、昵称、消息内容和创建时间。
用户可以删除自己的消息，删除操作需要确认。组件通过接收 props 传递数据，并在删除消息后发出事件通知父组件。-->
<template>
<div>
  <div style="float: left">
    <img :src="baseApi + message.avatar" class="avatar"/>
  </div>

  <div style="display: inline-block;overflow: hidden;width: 800px">
    <div>
      <span class="user">{{message.nickname}}</span>

      <el-popconfirm
          @confirm="delMessage"
          title="确定删除？"
      >
        <el-button style="font-size: 15px;float: right" slot="reference"  v-show="message.userId===userId">删除</el-button>
      </el-popconfirm>
    </div>
    <div style="margin: 12px 0">
      {{message.message}}
    </div>
    <span style="font-size: 10px">{{ message.createTime }}</span>
  </div>


</div>
</template>

<script>
export default {
  name: "MessageItem",
  props:{
    message: Object,
    userId: Number,
    index: Number,
  },
  data() {
    return {
      baseApi: this.$store.state.baseApi,
    }
  },
  created() {
  },
  methods:{
    delMessage(){
      console.log('del')
      this.request.delete("/api/market/message/"+this.message.id).then(res=>{
        if(res.code==='200'){
          this.$message.success("删除成功")
          this.$emit("del-message",this.index)
        }else {
          this.$message.error("删除失败")
        }
      })
    }
  }
}
</script>

<style scoped>
.avatar{
  width: 55px;
  height: 55px;
  border-radius: 50%;
  position: relative;
  top: 4px;
}
.user{
  font-size: 14px;
  font-weight: inherit;
  color: #f69090;
  position: relative;
  word-wrap: break-word;
  line-height: 16px;
}
</style>