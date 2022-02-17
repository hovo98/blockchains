<template lang="pug">

</template>

<script>
import * as Cookie from "tiny-cookie"
import MarkdownIt from "markdown-it"

export default {
  data() {
    return {
      md: new MarkdownIt({
        linkify: true,
        html: true
      }),
      show: null,
      url: "https://cosmos.network",
      content:
        "cosmos.network 2.0 has landed. <strong>Check it out</strong> &#8594;"
    }
  },
  mounted() {
    if (Cookie.get("cosmos-top-banner-hidden", false)) this.show = false
    else this.show = true
  },
  methods: {
    close() {
      this.show = false

      // reset every 2 days
      Cookie.set("cosmos-top-banner-hidden", true, { expires: "2D" })
    },
    beforeLeave(el) {
      el.style.marginTop = `-${el.offsetHeight}px`
    }
  }
}
</script>

<style lang="stylus" scoped>
/deep/
  strong
    color var(--white-100)
    font-weight 700

.banner
  display flex
  align-items stretch
  justify-content center
  position relative
  width 100%
  z-index 102

.banner__content
  font-size 0.875rem
  line-height 1.25rem
  letter-spacing 0.01em
  color var(--dark-txt)
  background linear-gradient(90deg, #CF36D2 0%, #F6743C 100%)
  text-align center
  display flex
  flex auto
  padding 0.75rem var(--pad320)
  align-items center
  justify-content center
  background-color #F8F9FC
  transition background-color 0.15s ease-out

  &:hover,
  &:focus
    background-color #F1F2F7
    opacity 0.96

.banner__dismiss
  position absolute
  top 0
  right 0
  bottom 0
  padding 0 1rem
  display flex
  align-items center

  &__icon
    padding 0.5rem
    border-radius 50%
    opacity 0.4
    transition opacity 0.15s ease-out, background-color 0.2s

    svg
      display block

  &:hover &__icon,
  &:focus &__icon
    opacity 0.7
    background-color rgba(0,0,0,0.1)

.fade-leave-active
  transition opacity 0.3s cubic-bezier(0.32, 0, 0.67, 0), margin 0.3s cubic-bezier(0.32, 0, 0.67, 0)

.fade-leave-to
  opacity 0

@media screen and (max-width: 414px)
  .banner__content
    text-align left
    justify-content flex-start
    padding-left 1rem
    padding-right 3rem

@media screen and (max-width: 320px)
  .banner__content
    font-size 0.8125rem
    line-height 1.125rem

  .banner__dismiss
    padding 0 0.5rem
</style>
