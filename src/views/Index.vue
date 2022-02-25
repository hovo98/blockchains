<template lang="pug">
div
  modal(v-bind="{visible: !!(video), side: 'center', buttonClose: true, fullscreen: true, width: '900px', backgroundColor: 'rgba(0,0,0,.8)'}" @visible="video = $event" v-if="!!(video)")
    div.modal__content(v-if="!!(video)")
      iframe(width="100%" height="510" src="https://www.youtube.com/embed/Eb8xkDi_PUg?autoplay=1&controls=1&rel=0&modestbranding=1&fs=1" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen)
  div
    tm-section#section-hero(theme="dark" layout="hero")
      div(slot="suptitle") Everything On Chain
      div(slot="title")
        .phone Join the #[strong most powerful] ecosystem of connected blockchains
        .tablet.laptop.desktop #[strong {{ adjectiveCurrent }}] #[br]  Simple scripts, on chain, in Python.
      div(slot="image")
        img.phone.tablet(src="~assets/images/home/section-hero-mobile.png" alt="Hero image")
        img.laptop(src="~assets/images/home/section-hero-desktop.png" alt="Hero image")
        img.desktop(src="~assets/images/home/section-hero-desktop.png" alt="Hero image")

    tm-section#section-problems(layout="center")
      div(slot="title") Made For Developers
      .tm-cards-issue

        tm-card-issue(icon="Secure")
          template(slot="problem-title") Simple, Secure Scripts In Python
          template(slot="problem-subtitle") Code in simple syntax that you're already used to. Dyson Protocol reads Python and outputs in REST / JSON. Dyson solves the difficult security problems that makes this impossible on other chains..

        tm-card-issue(icon="Interoperable")
          template(slot="problem-title") Fully Interoperable with the Cosmos Ecosystem
          template(slot="problem-subtitle") Dyson operates using the Cosmos SDK and Inter-Blockchain Communication Protocol. <br><br><br>

        tm-card-issue(icon="Build")
          template(slot="problem-title") Build A Decentralized Website or Web App
          template(slot="problem-subtitle") Dyson allows you to build serverless websites and DAPPs on the blockchain. Presentation and interface are distributed and built into the protocol. Everything is on chain.


        tm-card-issue(icon="Variable")
          template(slot="problem-title") Variable Fees
          template(slot="problem-subtitle") Transaction fees are based on the complexity of your script. Simple scripts = low fees.

        tm-card-issue(icon="Proof")
          template(slot="problem-title") Proof Of Stake
          template(slot="problem-subtitle") DYS is proof of stake. Validators can sleep well knowing mining DYS is low environmental impact.

        tm-card-issue(icon="Easy")
          template(slot="problem-title") Easy Development
          template(slot="problem-subtitle") DYS is designed for developers. Low learning curve. Use code you already know.


    tm-section#section-sdk(layout="split" theme="dark")
      div(slot="title") Why Dyson Protocol?
      p We're building an ecosystem that rewards contributors and early adopters. Our goal is to make it easy to program on the blockchain.<br>
      p How easy? This website is hosted on chain and the hosting is fully distributed.
      tm-btn(size="lg" value="See the script" type="link" :to="{ name: 'product-sdk' }"
        icon="arrow_forward" icon-pos="right")
      div(slot="image")
        .phone: img(src="~assets/images/home/section-sdk-mobile.svg" alt="SDK")
        .tablet: img(src="~assets/images/home/section-sdk-mobile.svg" alt="SDK")
        .laptop
        .desktop

    tm-section(layout="split" theme="stars")
      div(slot="title") About Dyson Protocol
      p Dyson Protocol is developed by Sybil Singleton, a distributed team that is passionate about blockchain technology and the future of web3. Dyson was born out of frustration with the current blockchain infrastructure. Most blockchain projects start with an ICO or IDO to raise money before any actual development. We decided to flip that script and show you our MVP first. Our goal is to build value in the DYS ecosystem to be shared among our community, validators, and developers.
      p Sybil Singleton is an AI / human / nanobot hybrid sent from the future to speed the progression of blockchain development. For what reason? We are not at liberty to say. 

</template>

<script>
import { mapGetters } from "vuex"
import TmBtn from "common/TmBtn"
import TmCardIssue from "cards/TmCardIssue"
import TmSection from "common/TmSection"
import { Modal } from "@cosmos-ui/vue"
import SectionLogos from "sections/SectionLogos"

export default {
  name: "page-index",
  metaInfo: { title: "Internet of Blockchains" },
  components: {
    SectionNews: () => import("sections/SectionNews"),
    SectionLogos,
    TmBtn,
    TmCardIssue,
    TmSection,
    Modal
  },
  computed: {
    ...mapGetters(["urls"])
  },
  data: function() {
    return {
      video: null,
      adjectiveId: 0,
      adjectives: ["A Blockchain For Developers."],
      adjectiveCurrent: "A Blockchain For Developers."
    }
  },
  mounted() {
    // setInterval(() => {
    //   if (this.adjectiveId === 4) {
    //     this.adjectiveId = 0
    //   }
    //   this.adjectiveCurrent = this.adjectives[this.adjectiveId]
    //   this.adjectiveId++
    // }, 2000)
    $(".image").css('z-index', -1);
    // $(".background-stars-container").css('background-image', 'url("/img/bg-d.81418c18.jpg")');
    // $(".background-stars-container").css('background-image', 'url("/assets/images/site/bg-d.jpg")');

  },
  methods: {
    videoPlay(bool) {
      this.$gtm.trackEvent({
        event: "event",
        category: "Video",
        action: "play",
        label: "Cosmos: The Vision",
        value: true
      })
      this.video = bool
    }
  },
}
</script>

<style lang="stylus" scoped>
@import '~variables'

/deep/
  @media screen and (max-width: 768px)
    .tm-section__text
      margin-top 8rem

img.stargate
  position absolute
  bottom 0
  right 24%
  max-width 59.9375rem
  height 34.8125rem
  width unset

.phone
  img.stargate
    left 90px

.modal__content
  background black
  width 100%
  line-height 0
  display flex
  align-items center
  height 100%

@media screen and (max-width: 1023px)
  img.stargate
    right auto
    left 24%
    bottom -10%

@media screen and (max-width: 767px)
  img.stargate
    right auto
    bottom -20%
    left 10%

@media screen and (max-width: 900px)
  .modal__content iframe
    max-height 75vh

#section-hero
  background: url('~images/site/header-new.png');
  background-repeat: no-repeat;
  background-size: cover;

  #section-validators .tm-section__image
  img
    width 53vw
    margin 0 auto

#section-sdk
  background:url('~images/site/bg-b.jpg')
  background-size: cover

@media screen and (min-width: 768px)
  #section-validators .tm-section__image
  #section-ethermint .tm-section__image
    img
      max-width 300px

  #section-sdk .tm-section__image
    img
      max-width 450px

@media screen and (min-width: 1920px)
  #section-explorer
    .tm-section__image
      padding-top var(--pad768)
      padding-bottom var(--pad768)
</style>
