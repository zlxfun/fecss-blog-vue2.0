<template>
  <div class="tags-container ly-col-14">
    <h1 class="tags-head-title">标签</h1>
    <div class="tags-wrap">
      <section class="tags">
        <h2 class="tags-year">{{tags}}</h2>
        <ul class="tags-list">
          <li class="tags-item"
            v-for="item in tagsContent">
            <span class="post-time">{{item.createTime}}</span>
            <router-link class="post-title-link"
              :to="{name: 'article', params: {id: item._id}}">
              {{item.title}}
            </router-link>
          </li>
        </ul>
      </section>
    </div>
  </div>
</template>

<script>
import { mapActions } from 'vuex'
export default {
  name: 'tagsContent',
  data() {
    return {
      tagsContent: []
    }
  },
  computed: {
    tags() {
      if (this.tagsContent[0]) {
        return this.tagsContent[0].tags
      }
      return ''
    },
    id() {
      return this.$route.params.id
    }
  },
  methods: {
    ...mapActions(['getTagsContent']),
    evtGetTagsContent() {
      this.getTagsContent(this.id).then((res) => {
        console.log(res)
        this.tagsContent = res.data.content
      })
    }
  },
  created () {
    this.evtGetTagsContent()
  }
}
</script>

<style scoped>
@import '../assets/css/animate.css';

.tags-container {
  box-sizing: border-box;
  min-height: 435px;
  margin-left: 30px;
  border-radius: 5px;
  background: #fff;
  box-shadow: 0px 5px 15px rgba(0, 0, 0, 0.12);
}
.tags-head-title {
  box-sizing: border-box;
  width: 100%;
  height: 55px;
  line-height: 55px;
  font-size: 16px;
  font-weight: normal;
  color: rgba(0, 0, 0, 0.4);
  padding: 0 30px;
  margin: 0;
  border-bottom: 1px solid #eee;
}
.tags-wrap {
  padding: 0 30px;
}
.tags {
  border-left: 2px solid #42b983;
  .tags-year {
    position: relative;
    padding-left: 10px;
    &::before {
      content: " ";
      position: absolute;
      left: 0;
      top: 12px;
      width: 10px;
      height: 10px;
      margin-left: -6px;
      background: #42b983;
      border-radius: 50%;
      border: 1px solid #fff;
    }
  }
  .tags-item {
    position: relative;
    padding: 10px 0;
    border-bottom: 1px dashed #ccc;
    &::before {
      content: " ";
      position: absolute;
      left: 0;
      top: 20px;
      width: 6px;
      height: 6px;
      margin-left: -4px;
      background: #42b983;
      border-radius: 50%;
      border: 1px solid #fff;
      transition: all 0.3s;
    }
    &:hover {
      &::before {
        background: #11a763;
      }
      & {
        border-bottom: 1px dashed #aaa;
      }
    }
    .post-time {
      position: absolute;
      left: 26px;
      top: 12px;
      font-size: 14px;
    }
    .post-title-link {
      display: block;
      font-size: 16px;
      margin-left: 140px;
      color: #42b983;
    }
  }
}
</style>
