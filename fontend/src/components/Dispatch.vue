<template>
  <div class="about-wrapper">
    <h2 class="list-title">发文</h2>
    <div class="comment-form">
      <input v-model="title" class="comment-form-name" type="text" placeholder="标题" maxlength="20">
      <input v-model="category" class="comment-form-name" type="text" placeholder="分类" maxlength="20">
      <input v-model="abstract" class="comment-form-name" type="text" placeholder="摘要" maxlength="20">
      <input v-model="tags" class="comment-form-name" type="text" placeholder="标签（前端暂未支持）" maxlength="20">
      <input v-model="password" class="comment-form-name" type="text" placeholder="发文码" maxlength="20">
      <textarea v-model="content" class="comment-form-content" name="" id="" cols="50" rows="15"
                placeholder="内容" debounce="500"></textarea>
      <div class="comment-item-reply-wrapper">
        <a @click="submit" class="comment-item-reply comment-item-reply-submit">发文</a>
      </div>
    </div>
    <h3 class="list-title">预览</h3>
    {{{ markedContent }}}
  </div>
</template>

<script type="text/babel">
  import marked from 'marked'
  import {updateHeadline, submitPost} from '../vuex/actions'

  export default {
    data () {
      return {
        title: '',
        abstract: '',
        category: '',
        tags: '',
        password: '',
        content: ''
      }
    },
    vuex: {
      actions: {
        updateHeadline,
        submitPost
      }
    },
    computed: {
      markedContent: function () {
        return marked(this.content)
      }
    },
    created () {
      this.updateHeadline('发文')
    },
    methods: {
      submit () {
        let data = {
          title: this.title,
          abstract: this.abstract,
          category: this.category,
          password: this.password,
          tags: [],
          content: this.content
        }
        // noinspection JSUnresolvedFunction
        this.submitPost(data)
      }
    }
  }
</script>

<style>
  .about-wrapper {
    width: 80%;
    padding: 1rem;;
  }

  .about-wrapper a {
    color: #4078c0;
    display: block;
    transition: all .4s;
  }

  .about-wrapper a:hover {
    color: #80b2ff;
  }

  .about-wrapper p, .about-wrapper h2, .about-wrapper a {
    margin: 1rem auto;
  }

  .about-wrapper p {
    font-size: 1.8rem;
  }

  .about-wrapper a {
    font-size: 1.6rem;
  }

  .comment-item-reply-wrapper {
    display: flex;
    flex-flow: row wrap;
    justify-content: flex-end;
  }

  .comment-item-reply {
    padding: 1rem;
    transition: all .4s;
  }

  .comment-item-reply:hover {
    color: #838383;
    cursor: pointer;
  }

  .comment-reply-container {
    border: 1px solid #d2d2d2;
    border-radius: .5rem;
    margin: 1rem;
    color: #7c7c7c;
  }

  .comment-reply-container .comment-item-title {
    background-color: #fbfbfb;
  }

  .comment-form {
    display: flex;
    flex-flow: column nowrap;
    padding: 1rem;
  }

  .comment-form-name, .comment-form-content {
    border: 1px solid #d2d2d2;
    margin-bottom: 1rem;
    padding: 1rem;
    font-size: 1.6rem;
    border-radius: .5rem;
  }

  .comment-form-name {
    height: 3.6rem;
  }

  .comment-form-content {
    resize: none;
  }

  .comment-item-reply-submit {
    border: 1px solid #d2d2d2;
    border-radius: .5rem;
  }

  @media screen and (max-width: 768px) {
    .about-wrapper p {
      font-size: 1.6rem;
    }
  }

  .content {
    margin: 2rem 1rem;
    display: flex;
  }

  .content pre {
    padding: 1rem;
    font: 14px consolas, "liberation mono", menlo, courier, monospace;
    background-color: #f7f7f7;
    white-space: pre-wrap;
    overflow: auto;
    max-width: 800px;
  }

  .content code {
    font: inherit;
  }

  .content table {
    border-collapse: collapse;
  }

  .content td, .post th {
    border: 1px solid #ddd;
    padding: .3rem .6rem;
  }

  .content tbody tr:nth-child(2n+1) {
    background-color: #f7f7f7;
  }

  .content a {
    color: #4078c0;
    transition: all .4s;
  }

  .content a:hover {
    color: #80b2ff;
  }

  .content img, .post code {
    max-width: 100%;
  }

  .content h1, .post h2 {
    border-bottom: 1px solid #d2d2d2;
    margin: 1rem 0;
  }

  .content ul {
    padding-left: 2rem;
  }

  .content li {
    list-style: disc;
  }

  .content p, .post {
    margin-bottom: 1rem;
    color: rgba(0, 0, 0, .8);
  }

  .content blockquote {
    padding: 0 1.5rem;
    margin: 0;
    color: #777;
    border-left: 4px solid #ddd;
  }

  @media screen and (max-width: 768px) {
    .content {
      padding: 1rem;
      margin: 0;
      font-size: 1.4rem;
    }

    .content h1 {
      font-size: 2.4rem;
    }

    .content h2 {
      font-size: 2.2rem;
    }

    .content h3 {
      font-size: 2rem;
    }

    .content pre {
      font-size: 1.2rem;
    }
  }
</style>
