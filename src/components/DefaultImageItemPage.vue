<template>
  <div id="patchouli-default-image-item-page">
    <DefaultImageItem
      v-for="(d, index) in defaultProcessedLibrary"
      v-show="index < imageToShowCount"
      :key="d.illustId"
      :img-url="getThumbUrl(d.urls)"
      :illust-id="d.illustId"
      :illust-title="d.illustTitle"
      :illust-page-count="d.illustPageCount"
      :is-ugoira="d.isUgoira"
      :user-name="d.userName"
      :user-id="d.userId"
      :profile-img-url="d.profileImg"
      :bookmark-count="d.bookmarkCount"
      :is-private-bookmark="d.isPrivateBookmark"
      :is-bookmarked="d.isBookmarked"
      :is-followed="d.isFollowed"
      :bookmark-id="d.bookmarkId"
    />
  </div>
</template>

<script>
import DefaultImageItem from './DefaultImageItem.vue';

export default {
  components: { DefaultImageItem },
  computed: {
    defaultProcessedLibrary() {
      const { shows, hides } = this.displayIndices;
      const iiLib = this.$store.getters['pixiv/imageItemLibrary'];

      return shows.concat(hides).map(idx => iiLib[idx]);
    },
    displayIndices() {
      return this.$store.getters['pixiv/defaultDisplayIndices'];
    },
    imageToShowCount() {
      const { shows } = this.displayIndices;
      return shows.length;
    },
  },
  methods: {
    getThumbUrl(urls) {
      if (this.$store.getters.config.croppedThumb) {
        return urls.thumb;
      }
      return urls.regular;
    },
  },
};
</script>

<style scoped>
#patchouli-default-image-item-page {
  display: flex;
  flex-flow: wrap;
  justify-content: space-around;
}
</style>


