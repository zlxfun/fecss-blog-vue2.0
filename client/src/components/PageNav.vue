<template>
  <div class="page-nav clearfix">
    <div class="page-nav-pre"
      v-if="startShow"
      @click="evtTogglePre">
      <i class="icon-pre ion-chevron-left"></i>
      上一页
    </div>
    <div class="page-nav-next"
      v-if="endShow"
      @click="evtToggleNext">
      下一页
      <i class="icon-next ion-chevron-right"></i>
    </div>
  </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
  computed: {
    ...mapGetters({
      maxIndex: 'maxIndex'
    }),
    startShow () {
      return this.start > 0
    },
    endShow () {
      return this.start < this.maxIndex
    }
  },
  props: {
    start: {
      type: Number,
      required: true
    }
  },
  methods: {
    ...mapActions(['getArticleList']),
    evtToggleNext () {
      this.$parent.evtToggleNext()
    },
    evtTogglePre () {
      this.$parent.evtTogglePre()
    }
  }
}
</script>

<style scoped>
.page-nav {
  width: 100%;
  height: 30px;
  .page-nav-pre, .page-nav-next {
    position: relative;
    width: 70px;
    height: 30px;
    line-height: 30px;
    text-align: center;
    font-size: 12px;
    color: #444;
    background: #fff;
    border: 1px solid rgba(0,0,0,.06);
    cursor: pointer;
    &:hover {
      background: rgba(0, 0, 0, 0.6);
      color: #f5f5f5;
    }
  }
  .page-nav-pre {
    float: left;
    .icon-pre {
      margin-right: 5px;
    }
  }
  .page-nav-next {
    float: right;
    .icon-next {
      margin-left: 5px;
    }
  }
}
</style>
