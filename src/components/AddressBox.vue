<!--
这个Vue组件 AddressBox 是一个用来显示地址信息的卡片。组件展示了联系人信息（包括联系人姓名、电话和地址），并提供了“修改”和“删除”两个操作链接，点击这些链接会触发父组件的相应事件。

代码结构
模板部分 (<template>)
  整个内容放在一个 div 标签中，类名为 box，并有一些内联样式。
  通过 address 对象的属性显示联系人姓名、电话和地址。
  提供两个操作链接：
  “修改”链接，点击时触发 edit 事件。
  “删除”链接，点击时触发 delete 事件。
  脚本部分 (<script>)
  定义了一个名为 AddressBox 的Vue组件。
接受一个 address 对象作为 props。
样式部分 (<style scoped>)
  为 box 类设置了样式，包括内边距、宽度、高度、边框、显示方式等。-->
<template>
<div class="box" style="position: relative;border-radius: 10px">
  <div>
    <span > {{address.linkUser}}</span>
  </div>
  <hr style="margin: 10px 0;font-size: 1px">
  <span> {{address.linkPhone}}</span>
  <span> {{address.linkAddress}}</span>
  <div style="margin-top: 5px">
    <a @click="$emit('edit')" style="color: #710a0a;cursor: pointer;position:absolute;bottom: 10px">修改</a>
    <a @click="$emit('delete')" style="color: #710a0a;cursor: pointer;float: right;position:absolute;bottom: 10px;right: 10px">删除</a>
  </div>
</div>
</template>

<script>
export default {
  name: "AddressBox",
  props:{
    address: Object,
  },
}
</script>

<style scoped>
.box{
  padding: 10px;
  width: 300px;
  height: 120px;
  display: inline-block;
  border: #333333 1px solid;
}

</style>

