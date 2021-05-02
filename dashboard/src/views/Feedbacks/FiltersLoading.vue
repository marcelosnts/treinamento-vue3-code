<template>
  <content-loader
    class="flex flex-col items-center rounded"
    width="100%"
    height="168px"
  >
    <content-loader
      class="mt-3 rounded"
      width="90%"
      height="32px"
      animation-duration="2s"
    />
    <content-loader
      class="mt-3 rounded"
      width="90%"
      height="32px"
      animation-duration="2s"
    />
    <content-loader
      class="mt-3 rounded"
      width="90%"
      height="32px"
      animation-duration="2s"
    />
    <content-loader
      class="mt-3 rounded"
      width="90%"
      height="32px"
      animation-duration="2s"
    />
  </content-loader>
</template>

<script>
import ContentLoader from '../../components/ContentLoader'

export default {
  components: { ContentLoader }
}
</script>
