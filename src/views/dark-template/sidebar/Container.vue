<template>
  <v-card
    color="grey darken-3"
    dark
  >
    <v-card-text>
      <avatar />
      <div class="text-sm-center mb-4 mt-3">
        <h1>
          <span class="light-blue--text text--lighten-3">Giang Phạm</span>
        </h1>
        <span>
          Bạn chỉ thật sự thất bại khi bạn từ bỏ mọi cố gắng.
        </span>
      </div>

      <sidebar-section :options="sections.info" />
      <sidebar-section :options="sections.socials" />
      <sidebar-section :options="sections.hobbies">
        <template v-slot:item="{item}">
          <v-chip>
            <v-avatar>
              <v-icon>
                {{ item.icon }}
              </v-icon>
            </v-avatar>
            {{ item.text }}
          </v-chip>
        </template>
      </sidebar-section>
      <sidebar-section :options="sections.languages">
        <template v-slot:items="{items}">
          <v-container pa-0>
            <v-layout
              wrap
              class="text-xs-center"
            >
              <template
                v-for="(item, i) in items"
              >
                <v-flex
                  :key="i"
                  md3
                  sm4
                  xs6
                >
                  <v-progress-circular
                    rotate="360"
                    size="90"
                    width="2"
                    :value="item.value"
                    color="white"
                    class="ma-2"
                  >
                    {{ item.text }}
                  </v-progress-circular>
                </v-flex>
              </template>
            </v-layout>
          </v-container>
        </template>
      </sidebar-section>
    </v-card-text>
  </v-card>
</template>

<script>
import Avatar from '@/views/dark-template/sidebar/Avatar'
import SidebarSection from '@/views/dark-template/sidebar/Section'
export default {
  name      : 'Sidebar',
  components: { SidebarSection, Avatar },
  data () {
    return {
      sections: {
        info: {
          title: 'THÔNG TIN',
          items: [
            {
              name: 'Email',
              icon: 'mdi-email',
              text: 'giangpham.1751996@gmail.com',
            },
            {
              name: 'Website',
              icon: 'mdi-web',
              text: 'giangpham.xyz',
            },
            {
              name: 'Birthday',
              icon: 'mdi-cake-variant',
              text: 'May 17, 1996',
            },
            {
              name: 'Live in',
              icon: 'mdi-map-marker',
              text: 'Ho Chi Minh City, Vietnam',
            },
          ],
        },
        socials: {
          title: 'MẠNG XÃ HỘI',
          items: [
            {
              icon: 'mdi-github-circle',
              text: 'github.com/giangpham175',
              link: 'https://github.com/giangpham175',
            },
            {
              icon: 'mdi-facebook',
              text: 'fb.com/GPluvheodat',
              link: 'https://www.facebook.com/GPluvheodat',
            },
          ],
        },
        hobbies: {
          title: 'SỞ THÍCH',
          items: [
            {
              icon: 'mdi-image-filter-hdr',
              text: 'Travel',
            },
            {
              icon: 'mdi-karate',
              text: 'Sports',
            },
            {
              icon: 'mdi-music',
              text: 'Music',
            },
            {
              icon: 'mdi-book-open-page-variant',
              text: 'Books',
            },
            {
              icon: 'mdi-television',
              text: 'Video games',
            },
          ],
        },
        languages: {
          title: 'NGÔN NGỮ',
          items: [
            {
              text : 'English',
              value: 45,
            },
            {
              text : 'Vietnamese',
              value: 90,
            },
          ],
        },
      },
    }
  },
}
</script>

<style scoped>
.sidebar{
    background: #2e2e2e;
}
</style>
