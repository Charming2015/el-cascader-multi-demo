<template>
  <div class="card" :style="`width: ${width}px`">
    <div class="title">
      {{title}}
    </div>
    <div class="content" style="height: calc(100% - 30px);overflow:auto;">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: {
      type: String
    },
    width: {
      type: Number,
      default: 220
    }
  }
}
</script>

<style>
p {margin: 0; padding: 0;}
.card {
  border: 1px solid #ddd;
  border-radius: 5px;
  min-height: 300px;
  margin-left: 10px;
  float: left;
}
.card .title {
  background: #ddd;
  height: 30px;
  line-height: 30px;
  text-indent: 1em;
  color: #fff;
  width: 100%;
}
.card .content {
  padding: 10px;
  box-sizing: border-box;
}

.card .content .label {
  width: 210px;
  display: inline-block;
  font-size: 14px;
}
</style>
