<!-- @format -->

<template>
  <div id="vditor" class="export-ppt" :class="{ fullScreen: isFullScreen }">
    <div class="reveal">
      <div class="slides" v-html="savedHtml" contenteditable="true">
        <!-- <section data-markdown data-separator="#---#" data-separator-vertical="#--#">
          <section data-template>
            {{ savedMdContent }}
          </section>
        </section> -->
      </div>
    </div>
  </div>
</template>

<script>
import Reveal from 'reveal.js/js/reveal'
import 'reveal.js/css/reset.css'
import 'reveal.js/css/reveal.css'
import 'reveal.js/css/theme/beige.css'

export default {
  name: 'export-ppt',

  data() {
    return {
      savedMdContent: '',
      savedHtml: '',
      isFullScreen: false
    }
  },

  created() {
    this.$utils.updateHtmlStyle()
    this.savedMdContent = localStorage.getItem('vditorvditor')
    this.savedHtml = localStorage.getItem('vditorHtml')
  },

  components: {},

  mounted() {
    this.initReveal()
    document.onfullscreenchange = evt => {
      this.isFullScreen = !!document.fullscreenElement
    }
  },

  methods: {
    initReveal() {
      window.Reveal = Reveal
      const revealSourcePath = `https://cdn.bootcss.com/reveal.js/3.8.0/`
      Reveal.initialize({
        controls: true,
        progress: true,
        center: true,
        hash: true,
        transition: 'slide',
        display: 'block',
        dependencies: [
          {
            src: `${revealSourcePath}/plugin/markdown/marked.js`,
            condition: function() {
              return !!document.querySelector('[data-markdown]')
            }
          },
          {
            src: `${revealSourcePath}/plugin/markdown/markdown.js`,
            condition: function() {
              return !!document.querySelector('[data-markdown]')
            }
          },
          // { src: `${revealSourcePath}/plugin/highlight/highlight.js`, async: true },
          { src: `${revealSourcePath}/plugin/search/search.js`, async: true },
          { src: `${revealSourcePath}/plugin/zoom-js/zoom.js`, async: true },
          { src: `${revealSourcePath}/plugin/notes/notes.js`, async: true }
        ]
      })
    }
    /* ---------------------Callback Event--------------------- */
  }
}
</script>

<style lang="less">
.export-ppt {
  width: 100%;
  .reveal {
    font-size: 2em;
    background-color: #ffffff;
    height: calc(100vh - 60px);
    h1 {
      font-size: 2em !important;
    }
    section {
      max-height: 100%;
      overflow: auto;
    }
  }
  &.fullScreen {
    .reveal {
      height: 100%;
    }
  }
}
</style>
