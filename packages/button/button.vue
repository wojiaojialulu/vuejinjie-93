<template>
  <!-- slot:插槽。 -->
  <div class="ui button" :class="cClass">
    <!-- 如果用户设置了icon属性，则显示图标 -->
    <i v-if="icon" class="icon" :class="icon"></i>
     <slot>我是默认内容</slot>
  </div>
  <!-- <div class="ui animated fade button">
    <div class="visible content">Sign-up for a Pro account</div>
    <div class="hidden content">
      $12.99 a month
    </div>
  </div> -->
</template>

<script>
export default {
  name: 'MyButton',
  props: {
    size: {
      type: String,
      default: 'medium',
      validator (val) {
        // 只要传入 size属性，就会
        // 进入到这个函数中，
        // 如返回true,则表示生效。
        // 如返回false，则表示不允许

        // 检验思路：
        // 如果传入的size是：mini,medium,huge,massive.... 就ok
        // 否则就返回false
        // console.log(val)
        // includes检查这个数组中，是否包含这个元素。
        return ['mini', 'tiny', 'small', 'medium', 'large', 'big', 'huge', 'massive'].includes(val)
      }
    },
    icon: {
      type: String,
      required: false
    },
    disabled: {
      type: Boolean,
      // 默认 不是 禁用状态
      default: false
    }
  },
  computed: {
    cClass () {
      // 收集收到的属性值，并分析一下
      // 返回class给按钮外层容器
      if (this.disabled) {
        // 用户开启禁用
        // disabled 是semantic-ui中一个特殊的class类名。
        // 这里就会有两个类名，所以加空格
        return this.size + ' ' + 'disabled'
      } else {
        return this.size
      }
    }
  }
}
</script>
