<template lang="pug">
  article.clover-item-border.rounded.overflow-hidden
    .relative.pb-ar-card
      header.absolute.col-12.top-0.left-0.pt2.px2
        h3.font-exp.h5.lh2 {{album.name}}
      figure.absolute.top-0.left-0.col-12(style="height:90%")
        .absolute.overlay.flex.items-end.justify-center(style="padding-bottom:24%")
          .col-7
            .relative.pb-100
              img.block.col-12.absolute.col-12.h-100.bottom-0(v-for="(clover, i) in album.clovers", v-if="i < 4", :src="cloverImage(clover, 128)", :style="{left: i * 22 + '%', zIndex: -1 * i, borderRadius: '100%', boxShadow: '0px 0px 2px rgba(255,255,255,0.75)'}")
      footer.absolute.bottom-0.left-0.col-12.px2.pb2.flex.justify-between
        h6.col-9.truncate.h5 {{_userName}}
        .col-4.flex.items-center.justify-end
          span.h5.font-mono {{album.clovers.length}}
          //- img.block(src="@/assets/icons/clover-icon-1.svg", style="width:0.66em; margin-left:0.175em")
</template>

<script>
import { cloverImage } from '@/utils'
import { mapGetters } from 'vuex'
export default {
  name: 'AlbumItem--Card',
  props: ['album'],
  computed: {
    ...mapGetters(['userName']),
    _userName () {
      return this.userName(this.album.user)
    },
    clovers () {
      console.log('compute clovers')
      // show most recent first
      const clvrs = JSON.parse(JSON.stringify(this.album.clovers))
      return clvrs.reverse()
    }
  },
  methods: {
    cloverImage
  }
}
</script>

<style>
</style>
