<template>
  <v-card
    color="grey lighten-4"
    light
  >
    <v-card-text>
      <content-section
        title="Tôi là ai?"
      >
        Tôi là 1 developer, chủ yếu tập trung vào front-end nhưng song song đó cũng có tìm hiểu thêm về back-end.
        <br><br>
        Áp dụng những vốn kiến thức đã có từ môi trường đại học cũng như vốn kiến thức từ thực tế, từ mạng lưới
        internet rộng lớn và tìm hiểu về nhu cầu thị trường để mang đến nhiều sản phẩm có giá trị sử dụng cho
        khách hàng, cho thị trường.
        <br>
        Từ đó giúp các sản phẩm mà tôi tham gia phát triển hơn được các sản phẩm của mình, giúp hài lòng
        khách hàng với sản phẩm của họ.
      </content-section>
      <content-section
        v-if="prouds"
        title="Tôi đã làm những gì?"
      >
        <v-layout
          v-for="(proud, i) in prouds"
          :key="i"
        >
          <v-flex
            md1
            xs3
          >
            <v-icon right>
              {{ proud.icon }}
            </v-icon>
          </v-flex>
          <v-flex
            md11
            xs9
          >
            <p>
              <strong>{{ proud.text }}</strong><br>
              <small>{{ proud.source }}</small>
            </p>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section
        v-if="educations"
        title="Học vấn và kinh nghiệm làm việc"
      >
        <v-layout
          v-for="(education, i) in educations"
          :key="i"
        >
          <v-flex md4>
            {{ education.from }} - {{ education.to }}
          </v-flex>
          <v-flex md8>
            <strong v-if="education.title">{{ education.title }}</strong>
            <div v-if="education.location">
              <i>{{ education.location }}</i>
            </div>
            <div v-if="education.description">
              {{ education.description }}
            </div>
            <br>
          </v-flex>
        </v-layout>
      </content-section>
      <content-section
        v-if="skills"
        id="to-timeline"
        title="Kỹ năng"
      >
        <!-- <template slot="actions">
          (% are relative not absolute)
        </template> -->
        <v-layout wrap>
          <template
            v-for="(skill, i) in skills"
          >
            <v-flex
              v-if="skill.divider"
              :key="i"
              md12
              xs12
              mb-4
            />
            <v-flex
              v-else
              :key="i"
              md6
              xs12
            >
              <div
                class="mr-2 ml-2"
              >
                <div class="align-center">
                  <v-icon
                    small
                  >
                    {{ skill.icon }}
                  </v-icon>
                  {{ skill.title }}
                </div>
                <v-progress-linear
                  class="progress"
                  color="secondary"
                  height="3"
                  :value="skill.value"
                />
              </div>
            </v-flex>
          </template>
        </v-layout>
      </content-section>
    </v-card-text>
  </v-card>
</template>

<script>
import ContentSection from '@/views/dark-template/content/Section'
export default {
  name      : 'MainContent',
  components: { ContentSection },
  data      : () => ({
    prouds: [
      {
        icon  : 'mdi-developer-board',
        text  : 'DevConnector',
        source: 'Trang web kết nối các lập trình viên',
      },
      // {
      //   icon  : 'mdi-library-music',
      //   text  : 'Made people enjoy and learn a new language for equivalent of 29+ years (older than myself!)',
      //   source: '(Bobet.ir and its channel downloads)',
      // },
      {
        icon  : 'mdi-timer-sand',
        text  : 'Soft skills',
        source: 'Tham gia nhiều các hoạt động công tác xã hội cũng như trau dồi kỹ năng mềm',
      },
    ],
    educations: [
      {
        from    : '2019',
        to      : '2020',
        title   : 'Font-end Developer',
        location: 'Công ty Công nghệ truyền thông METECH',
      },
      {
        from    : '2019',
        to      : '2019',
        title   : 'Manual Tester',
        location: 'FPT Software',
      },
      {
        from    : '2014',
        to      : '2019',
        title   : 'Công Nghệ Thông Tin',
        location: 'Đại học Sư phạm Kỹ thuật TP.HCM',
        // description: 'Became a member of University Academic Association of Computer Science',
      },
    ],
    skills: [
      {
        title: 'HTML5',
        icon : 'mdi-language-html5',
        value: 80,
      },
      {
        title: 'CSS3',
        icon : 'mdi-language-css3',
        value: 70,
      },
      { divider: true },
      {
        title: 'JavaScript',
        icon : 'mdi-language-javascript',
        value: 50,
      },
      {
        title: 'Vue.js Framework',
        icon : 'mdi-vuejs',
        value: 40,
      },
      { divider: true },
      {
        title: 'Boostrap 4',
        icon : 'mdi-alpha-b-box',
        value: 70,
      },
      {
        title: 'Git',
        icon : 'mdi-git',
        value: 67,
      },
      { divider: true },
      {
        title: 'NodeJS',
        icon : 'mdi-nodejs',
        value: 20,
      },
      { divider: true },
    ],
  }),
}
</script>

<style scoped>
.title {
  border-bottom: 2px #bfbfbf solid;
  line-height: 1.5 !important;
}
.progress {
  margin-top: 0.1rem;
}
</style>
