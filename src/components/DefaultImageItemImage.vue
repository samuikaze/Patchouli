<template>
  <div class="image-item-image">
    <a
      class="image-flexbox"
      rel="noopener"
      :href="illustPageUrl" >

      <div class="top-right-slot" v-if="illustPageCount > 1">
        <span><span class="multiple-icon"/>
        {{ illustPageCount }}</span>
      </div>

      <img :data-src="imgUrl" :src="imgUrl">
      <div class="ugoira-icon" v-if="isUgoira"/>
    </a>
    <div
      class="_one-click-bookmark"
      data-type="illust"
      data-click-action="illust"
      :class="{on:selfIsBookmarked}"
      :data-click-label="illustId"
      :data-id="illustId"
      :title="selfIsBookmarked"
      @click="oneClickBookmarkAdd"/>
      <!-- <div class="bookmark-input-container" v-if="bookmarkId">
      <input name="book_id[]" :value="bookmarkId" type="checkbox">
    </div> -->
  </div>
</template>

<script>
export default {
  props: {
    imgUrl: {
      type: String,
      default: ""
    },
    illustId: {
      type: String,
      default: ""
    },
    illustPageCount: {
      type: Number,
      default: 1
    },
    isUgoira: {
      type: Boolean,
      default: false
    },
    isBookmarked: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      selfIsBookmarked: this.isBookmarked
    };
  },
  computed: {
    illustPageUrl() {
      return `/member_illust.php?mode=medium&illust_id=${this.illustId}`;
    }
  },

  methods: {
    oneClickBookmarkAdd() {
      if (!this.selfIsBookmarked) {
        this.selfIsBookmarked = true;
      }
    }
  }
};
</script>

<style scoped>
.image-item-image {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}
.image-flexbox {
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  -webkit-box-orient: vertical;
  -webkit-box-direction: normal;
  -webkit-flex-flow: column;
  flex-flow: column;
  -webkit-box-pack: center;
  -webkit-justify-content: center;
  justify-content: center;
  -webkit-box-align: center;
  -webkit-align-items: center;
  align-items: center;
  z-index: 0;
  border: 1px solid #000;
  border: 1px solid rgba(0, 0, 0, 0.04);
  min-width: 88px;
  min-height: 88px;
  position: relative;
}
.top-right-slot {
  -webkit-box-flex: 0;
  -webkit-flex: none;
  flex: none;
  display: -webkit-box;
  display: -webkit-flex;
  display: flex;
  -webkit-box-align: center;
  -webkit-align-items: center;
  align-items: center;
  z-index: 1;
  box-sizing: border-box;
  margin: 0 0 -24px auto;
  padding: 6px;
  height: 24px;
  background: #000;
  background: rgba(0, 0, 0, 0.4);
  border-radius: 0 0 0 4px;
  color: #fff;
  font-size: 12px;
  line-height: 1;
  font-weight: 700;
}
.multiple-icon {
  display: inline-block;
  margin-right: 4px;
  width: 10px;
  height: 10px;
  background: url(https://source.pixiv.net/www/js/bundle/3b9b0b9e331e13c46aeadaea83132203.svg);
}
.ugoira-icon {
  position: absolute;
  -webkit-box-flex: 0;
  -webkit-flex: none;
  flex: none;
  width: 40px;
  height: 40px;
  background: url(https://source.pixiv.net/www/js/bundle/f608d897f389e8161e230b817068526d.svg)
    50% no-repeat;
  top: 50%;
  left: 50%;
  margin: -20px 0 0 -20px;
}
img {
  max-height: 100%;
  max-width: 100%;
}
._one-click-bookmark {
  right: 0;
  width: 24px;
  height: 24px;
  line-height: 24px;
  z-index: 2;
  text-align: center;
  cursor: pointer;
  background: url(https://source.pixiv.net/www/images/bookmark-heart-off.svg)
    center transparent;
  background-repeat: no-repeat;
  background-size: cover;
  opacity: 0.8;
  filter: alpha(opacity=80);
  transition: opacity 0.2s ease-in-out;
}
._one-click-bookmark.on {
  background-image: url(https://source.pixiv.net/www/images/bookmark-heart-on.svg);
}
</style>

