<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text class="text-xs-center">
      <h4>Hmm... Chắc là CV của tôi dừng tại đây, tôi rất mong có thể cùng bạn làm được nhiều hơn nữa!</h4>
      <div>Nhưng... tiếp tục kéo xuống nhé!</div>
      <content-section>
        <v-timeline>
          <v-timeline-item
            v-for="n in futurePage * 2"
            :key="n"
            icon=""
            large
          >
            <template
              v-slot:icon
            >
              <div class="fill-width">
                <vue-content-loading
                  :width="80"
                  :height="95"
                >
                  <circle
                    cx="40"
                    cy="52"
                    r="42"
                  />
                </vue-content-loading>
              </div>
            </template>

            <vcl-code />
          </v-timeline-item>
        </v-timeline>
      </content-section>
      <div
        v-if="toggleMessage"
        class="ma-4"
      >
        <span
          class="pre"
        >{{ message.text }}</span>
        <div
          v-if="!loading"
          v-scroll="scrolled"
        />
      </div>
      <v-progress-circular
        v-if="loading"
        indeterminate
        color="primary"
      />
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
import VueContentLoading, { VclCode } from 'vue-content-loading'
import { debounce } from 'lodash'

export default {
  name      : 'EndlessTimeline',
  components: {
    ContentSection, VueContentLoading, VclCode,
  },
  data: () => ({
    futurePage   : 0,
    message      : '',
    toggleMessage: true,
    loading      : false,
    messages     : [
      {
        text: 'Ok, đây là dự định của tôi!',
        from: 1,
        to  : 1,
      },
      {
        text: 'và thêm nhiều nữa ... :)',
        from: 2,
        to  : 2,
      },
      {
        text: 'Muốn nữa chứ?',
        from: 3,
        to  : 3,
      },
      {
        text: 'Bạn có đang tò mò về thứ bên dưới?',
        from: 4,
        to  : 4,
      },
      {
        text: '...',
        from: 5,
        to  : 5,
      },
      {
        text: 'Chúng ta có thể làm mọi thứ!',
        from: 6,
        to  : 6,
      },
      {
        text: 'Những tin tức thú vị đây:',
        from: 7,
        to  : 7,
      },
      {
        text: 'kéo xuống nữa nào!',
        from: 8,
        to  : 8,
      },
      {
        text: 'nữa đi... kéo xuống nhiều hơn nữa...',
        from: 9,
        to  : 9,
      },
      {
        text: 'thật tốt khi bạn vẫn tiếp tục xem những gì bên dưới...',
        from: 10,
        to  : 10,
      },
      {
        text: 'mệt rồi... tạm nghỉ tay thôi 👌',
        from: 11,
        to  : null,
      },
    ],
  }),
  methods: {
    scrolled (event) {
      let element   = event.target
      if (!element.scrollTop)
        element = element.documentElement
      // TODO: it's not working correctly on mobile
      if (element.scrollHeight - element.scrollTop <= element.clientHeight + 50)
        this.loadFuture()
    },
    loadFuture: debounce(function () {
      if (this.loading || this.message.to === null)
        return
      this.loading = true
      setTimeout(() => {
        this.loading    = false
        this.futurePage++
        if (!this.message)
          this.message = this.messages[0]
        else if (this.message.to !== null && this.message.to < this.futurePage)
          this.message = this.messages.find((msg) => { return msg.from === this.futurePage })
        else {

        }
        this.toggleMessage = false
        this.toggleMessage = true
      }, 3000)
    }, 500),
  },
}
</script>

<style scoped>
.fill-width {
  width: 100%;
}
.pre {
  white-space: pre;
}
</style>
