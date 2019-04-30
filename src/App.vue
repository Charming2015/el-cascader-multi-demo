<template>
  <div id="app">
    <card title="配置(悬浮显示注释)" :width="320">
      <p class="per-line" title="是否只有叶子节点才支持多选">
        <label class="label">only-last({{onlyLast}})</label>:
        <el-switch v-model="onlyLast"></el-switch>
      </p>

      <p class="per-line" title="绑定的value的格式">
        <label class="label">is-two-dimension-value({{isTwoDimensionValue}})</label>:
        <el-switch v-model="isTwoDimensionValue"></el-switch>
      </p>
      
      <p class="per-line" title="是否禁用">
        <label class="label">disabled({{disabled}})</label>:
        <el-switch v-model="disabled"></el-switch>
      </p>
      
      <p class="per-line" title="是否可搜索">
        <label class="label">filterable({{filterable}})</label>:
        <el-switch v-model="filterable"></el-switch>
      </p>
      
      <p class="per-line" title="多选时是否将选中值按文字的形式展示">
        <label class="label">collapse-tags({{collapseTags}})</label>:
        <el-switch v-model="collapseTags"></el-switch>
      </p>
      
      <p class="per-line" title="是否支持清空选项">
        <label class="label">clearable({{clearable}})</label>:
        <el-switch v-model="clearable"></el-switch>
      </p>

      
      <p class="per-line" title="次级菜单的展开方式">
        <label class="label">expand-trigger</label>:
        <el-select v-model="expandTrigger" size="mini" style="width:80px;">
          <el-option value="click"></el-option>
          <el-option value="hover"></el-option>
        </el-select>
      </p>
      <p class="per-line" title="选项分隔符">
        <label class="label">separator</label>:
        <el-input v-model="separator" size="mini" style="width:80px;"></el-input>
      </p>
    </card>
    <card title="预览" style="max-height: 100%;">
      <el-cascader-multi
        v-if="hackReset"
        v-show="isTwoDimensionValue"
        v-model="checkList"
        :is-two-dimension-value="true"
        :data="options"
        :onlyLast="onlyLast"
        :disabled="disabled"
        :filterable="filterable"
        :collapse-tags="collapseTags"
        :clearable="clearable"
        :expand-trigger="expandTrigger"
        :separator="separator"
      >
      </el-cascader-multi>
      <el-cascader-multi
        v-if="hackReset"
        v-show="!isTwoDimensionValue"
        v-model="checkList2"
        :is-two-dimension-value="false"
        :data="options"
        :onlyLast="onlyLast"
        :filterable="filterable"
        :collapse-tags="collapseTags"
        :clearable="clearable"
        :expand-trigger="expandTrigger"
        :separator="separator"
      >
      </el-cascader-multi>
    </card>
    <card title="data(备选项)" :width="260" style="max-height: 100%;">
      <pre>
        [
          {
            value: 'zhinan',
            label: '指南',
            children: [{
              value: 'shejiyuanze',
              label: '设计原则',
              children: [{
                value: 'yizhi',
                label: '一致'
              }, {
                value: 'fankui',
                label: '反馈'
              }, {
                value: 'xiaolv',
                label: '效率'
              }, {
                value: 'kekong',
                label: '可控'
              }]
            }, {
              value: 'daohang',
              label: '导航',
              children: [{
                value: 'cexiangdaohang',
                label: '侧向导航'
              }, {
                value: 'dingbudaohang',
                label: '顶部导航'
              }]
            }]
          }, {
            value: 'ziyuan',
            label: '资源',
            children: [{
              value: 'axure',
              label: 'Axure Components'
            }, {
              value: 'sketch',
              label: 'Sketch Templates'
            }, {
              value: 'jiaohu',
              label: '组件交互文档'
            }]
          }
        ]
      </pre>
    </card>
    <card title="value(选中项)" :width="360" style="max-height: 100%;">
      <p>
        {{JSON.stringify(isTwoDimensionValue ? checkList : checkList2)}}
      </p>
    </card>
  </div>
</template>

<script>
import card from './components/card.vue'
export default {
  name: 'app',
  components: {
    card
  },
  watch: {
    separator() {
      this.hackReset = false
      this.$nextTick(() => {
        this.hackReset = true
      })
    }
  },
  data () {
    return {
      onlyLast: false,
      isTwoDimensionValue: true,
      disabled: false,
      filterable: false,
      collapseTags: false,
      clearable: false,
      separator: '/',
      expandTrigger: 'click',
      checkList2: ['yizhi'],
      checkList: [
        ['zhinan', 'shejiyuanze', 'yizhi'],
      ],
      options: [
        {
          value: 'zhinan',
          label: '指南',
          children: [{
            value: 'shejiyuanze',
            label: '设计原则',
            children: [{
              value: 'yizhi',
              label: '一致'
            }, {
              value: 'fankui',
              label: '反馈'
            }, {
              value: 'xiaolv',
              label: '效率'
            }, {
              value: 'kekong',
              label: '可控'
            }]
          }, {
            value: 'daohang',
            label: '导航',
            children: [{
              value: 'cexiangdaohang',
              label: '侧向导航'
            }, {
              value: 'dingbudaohang',
              label: '顶部导航'
            }]
          }]
        }, {
          value: 'ziyuan',
          label: '资源',
          children: [{
            value: 'axure',
            label: 'Axure Components'
          }, {
            value: 'sketch',
            label: 'Sketch Templates'
          }, {
            value: 'jiaohu',
            label: '组件交互文档'
          }]
        }
      ],
      hackReset: true
    }
  }
}
</script>

<style>
html,body{
  width: 100%;
  height: 100%;
  overflow: hidden;
  margin: 0;
  padding: 5px;
  box-sizing: border-box;
}
#app {
  width: 100%;
  height: 100%;
}
.per-line {
  margin-bottom: 10px;
  
}
.per-line label {
  cursor: pointer;
}
</style>
