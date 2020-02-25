<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        id="timeline"
        :title="detailed ? 'Cuộc sống' : 'Kinh nghiệm'"
      >
        <template slot="actions">
          <div>
            <v-switch
              v-model="detailed"
              :label="detailed ? 'Chi tiết' : 'Ngắn gọn'"
            />
          </div>
        </template>

        <v-timeline
          dense
        >
          <v-timeline-item
            v-for="(item, i) in orderedItems"
            :key="i"
            :icon="item.icon || ''"
            :class="{transparent: item.transparent}"
            large
          >
            <template
              v-if="item.iconImage"
              v-slot:icon
            >
              <v-avatar>
                <img
                  :src="publicPath(item.iconImage)"
                >
              </v-avatar>
            </template>
            <template v-slot:opposite />
            <v-layout>
              <v-flex
                v-if="$vuetify.breakpoint.smAndUp"
                md1
                sm2
                align-self-center
              >
                <span>{{ item.year }}</span>
              </v-flex>
              <v-flex
                md11
                sm10
                xs12
              >
                <v-card class="elevation-1">
                  <v-card-title class="pb-0">
                    <div>
                      <p v-if="$vuetify.breakpoint.xsOnly">
                        {{ item.year }}
                      </p>
                      <h3>{{ item.title }}</h3>
                    </div>
                  </v-card-title>
                  <v-card-text>
                    <v-layout wrap>
                      <v-flex
                        :md7="!!item.image"
                        :md12="!item.image"
                        xs12
                      >
                        <div class="mr-1">
                          <span
                            v-if="item.text"
                            class="pre"
                          >{{ item.text }}</span>
                          <!-- eslint-disable vue/no-v-html -->
                          <div
                            v-else-if="item.html"
                            v-html="item.html"
                          />
                          <!-- eslint-enable vue/no-v-html -->
                        </div>
                      </v-flex>
                      <v-flex
                        v-if="item.image"
                        md5
                        xs12
                      >
                        <div
                          class="mt-2"
                        >
                          <v-carousel
                            v-if="Array.isArray(item.image)"
                            :show-arrows="false"
                            :height="325"
                          >
                            <v-carousel-item
                              v-for="(citem,ci) in item.image"
                              :key="ci"
                              :src="publicPath(citem)"
                            />
                          </v-carousel>
                          <v-img
                            v-else
                            :max-height="item.imageHeight ? item.imageHeight : ''"
                            :src="publicPath(item.image)"
                          />
                        </div>
                      </v-flex>
                    </v-layout>
                  </v-card-text>
                </v-card>
              </v-flex>
            </v-layout>
          </v-timeline-item>
        </v-timeline>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'Timeline',
  components: { ContentSection },
  data      : () => ({
    detailed: true,
    items   : [
      {
        year : '2019',
        title: 'Website Dạy học',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Open Sourced</span><br>
              Available on: <a target="_blank" href="https://github.com/giangpham175/teach-web">giangpham175/teach-web</a>
          </p>
          <p>
            - Giúp các giáo viên và học sinh có thể giảng dạy và online, được xây dựng theo mô hình MVC. 
          </p>
          <p>
            - Trang web còn có thể sử dụng để làm kênh mà mọi người có thể bán chất xám của họ thông qua các video khóa học của họ làm ra, 
            cũng như cho những người cần những kiến thức mà họ đang tìm kiếm có thể tìm mua chúng.
          </p>
        `,
        image: 'img/timeline/teach-web.png',
        icon : 'mdi-github-circle',
      },
      {
        year : '2019',
        title: 'Website Quản lý hộ chiếu',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Open Sourced</span><br>
              Available on: <a target="_blank" href="https://github.com/giangpham175/passport-manager">giangpham175/passport-manager</a>
          </p>
          <p>
            - Giúp người dùng đăng ký, xét duyệt và quản lý hộ chiếu online, được xây dựng theo mô hình MVC. 
          </p>
          <p>
            - Project này để đảm bảo thực hiện phân quyền, giới hạn quyền cho mỗi đối tượng sử dụng, 
            nhằm đảm bảo mức độ bảo mật của dữ liệu, cũng như quy trình thực hiện của các đối tượng sử dụng cơ sở dữ liệu đó.
          </p>
        `,
        image: 'img/timeline/passport-manager.png',
        icon : 'mdi-github-circle',
      },
      {
        year : '2019',
        title: 'Website Kết nối Lập trình viên',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Published</span> on <a target="_blank" href="https://blooming-depths-78811.herokuapp.com/">DevConnector</a>
              <br>Available on: <a target="_blank" href="https://github.com/giangpham175/dev-connector">giangpham175/dev-connector</a>
          </p>
          <p>
            - Đây là nơi mà các dev có thể trao đổi các vấn đề, học hỏi lẫn nhau. Project được xây dựng theo mô hình MVC.
          </p>
          <p>
            - Project sử dụng ngôn ngữ JavaScript và bộ Open source công nghệ liên quan đến JavaScript và cũng là các công nghệ hot hiện nay bao gồm MongoDB, ExpressJS, React và NodeJS.
          </p>
          <p>
            - Vai trò:
            <ul>
                <li>Phân tích và lập trình</li>
                <li>Phát triển code</li>
            </ul>
          </p>
        `,
        image    : 'img/timeline/web-connector.png',
        iconImage: 'img/timeline/web-connector-logo.png',
      },
      {
        year : '2020',
        title: 'Shop Golike',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Published</span><br>
              Available on: <a target="_blank" href="http://shop.golike.net/">shop.golike.net</a>
          </p>
          <p>
            - Trang đặt mua áo online.
          </p>
          <p>
            - Và nếu bạn quan tâm, bạn có thể ghé xem các landingpage để hiểu hơn về UI của tôi:
            <ul>
                <li><a target="_blank" href="http://mualike.me/">mualike.me</a></li>
                <li><a target="_blank" href="http://mualike.site/">mualike.site</a></li>
                <li><a target="_blank" href="http://golike.site/">golike.site</a></li>
            </ul>
          </p>
        `,
        image: 'img/timeline/shop-golike.png',
        icon : 'mdi-github-circle',
      },
      {
        year : '2020',
        title: 'Resume Web',
        html : `
          <p>
              Current status: <span class="light-blue--text lighten-3">Open Sourced</span><br>
              Available on: <a target="_blank" href="https://github.com/giangpham175/vue-resume">giangpham175/vue-resume</a>
          </p>
          <p>
            - Trang web xây dựng dựa trên Vue framework nhằm tạo nên CV giới thiệu bản thân đến các nhà tuyển dụng.
          </p>
        `,
        image: 'img/timeline/vue-resume.png',
        icon : 'mdi-github-circle',
      },
    ],
  }),
  computed: {
    orderedItems () {
      const items = [...this.items].reverse()
      if (this.detailed)
        return items
      return items.filter((item) => {
        return !item.detailed
      })
    },
  },
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.pre {
  white-space: pre;
}
.transparent{
  opacity: 0.6;
}
</style>
