<template>
  <div class="d-flex flex-column align-center">
    <h1 class="mx-auto my-4">Workshop_01</h1>
    <v-sheet class="mx-auto" elevation="8" max-width="100%" style="width: 60%">
      <v-window v-model="model" class="pa-4" show-arrows>
        <!-- Info Card -->
        <v-window-item key="info" class="align-self-center">
          <v-card class="ma-4" :height="cardHeight" :width="cardWidth">
            <v-img
              src="https://scontent.fbkk27-1.fna.fbcdn.net/v/t1.18169-9/26731509_535298243518109_4064534849271455381_n.jpg?_nc_cat=106&ccb=1-7&_nc_sid=53a332&_nc_eui2=AeHQNqbFIJKR5N5mlVEgpEU9RKllLb90dR9EqWUtv3R1H-GOhgoi5K9qPg7QMCDpOQZfIBaz3ZDGqEOLz855VwJg&_nc_ohc=nxS3l5jSWe8Q7kNvgErND1H&_nc_ht=scontent.fbkk27-1.fna&oh=00_AYAeSJ88FNvdJxYp7Kl52hh0eCfdg8m2fyt5n1LmedoZiQ&oe=66DBEA0D"
              height="300px"
            />
            <v-card-title>About Me</v-card-title>
            <v-card-subtitle>Hello I'm Phoom. </v-card-subtitle>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="orange lighten-2" text @click="toggleShow('info')"
                >Read More</v-btn
              >
            </v-card-actions>
            <v-expand-transition>
              <div v-show="show.info">
                <v-divider></v-divider>
                <v-card-text>Name: Thidtanai Kaewphet </v-card-text>
                <v-card-text>Nick name: Phoom </v-card-text>
                <v-card-text>Email: thidtanai.k@gmail.com </v-card-text>
                <v-card-text>Facebook: Thidtanai Kaewphet </v-card-text>
                <v-card-text>Instagram: Thid_slowlife </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-window-item>

        <!-- Study -->
        <v-window-item key="study" class="align-self-center">
          <v-card class="ma-4" :height="cardHeight" :width="cardWidth">
            <v-img
              src="https://cdn-webs.pharmacy.cmu.ac.th/pharmacy/post-attatchment/01HQ5DZRC3VQHN647HFDMTXQQZ.jpg"
              height="300px"
            />
            <v-card-title>Education and Work</v-card-title>
            <v-card-subtitle>About my education and working.</v-card-subtitle>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="orange lighten-2" text @click="toggleShow('study')"
                >Read More</v-btn
              >
            </v-card-actions>
            <v-expand-transition>
              <div v-show="show.study">
                <v-card-text>
                  <div class="font-weight-bold ml-8 mb-2">Today</div>

                  <v-timeline align-top dense>
                    <v-timeline-item
                      v-for="message in messages"
                      :key="message.time"
                      :color="message.color"
                      small
                    >
                      <div>
                        <div class="font-weight-normal">
                          <strong>{{ message.from }}</strong> @{{
                            message.time
                          }}
                        </div>
                        <div>{{ message.message }}</div>
                      </div>
                    </v-timeline-item>
                  </v-timeline>
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-window-item>

        <!-- Other Card -->
        <v-window-item key="Others" class="align-self-center">
          <v-card class="ma-4" :height="cardHeight" :width="cardWidth">
            <v-img
              src="https://www.casita.com/images/files/public/05072023011757PM-shutterstock_2136659695.jpg"
              height="300px"
            />
            <v-card-title>Other</v-card-title>
            <v-card-subtitle>Know me more.</v-card-subtitle>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="orange lighten-2" text @click="toggleShow('others')"
                >Read More</v-btn
              >
            </v-card-actions>
            <v-expand-transition>
              <div v-show="show.others">
                <v-divider></v-divider>
                <div v-show="show.others_selection === 1">
                  <v-card-title>งานอดิเรก </v-card-title>
                  <ul>
                    <li><v-card-text>เล่นเกม</v-card-text></li>
                    <li><v-card-text>ดูอนิเมะ</v-card-text></li>
                    <li><v-card-text>ซักผ้า</v-card-text></li>
                  </ul>
                </div>
                <div v-show="show.others_selection === 2">
                  <v-card-title>ความชอบ </v-card-title>
                  <ul>
                    <li>
                      <v-card-text
                        >เกม: Osu, Project Zomboid, Civ6, HSR, ZZZ</v-card-text
                      >
                    </li>
                    <li>
                      <v-card-text
                        >อนิเมะ: Attack on titan, Re:zero, Bocchi the rock,
                        Dungeon Meshi</v-card-text
                      >
                    </li>
                    <li>
                      <v-card-text
                        >ศิลปิน: Minami, Zuttomayo, Ado, A7x, BMTH,
                        I9K</v-card-text
                      >
                    </li>
                  </ul>
                </div>
                <v-chip-group
                  v-model="show.others_selection"
                  active-class="deep-purple accent-4 white--text"
                  column
                  mandatory
                >
                  <v-chip :key="1" :value="1">งานอดิเรก</v-chip>

                  <v-chip :key="2" :value="2">ความชอบ</v-chip>
                </v-chip-group>
              </div>
            </v-expand-transition>
          </v-card>
        </v-window-item>

        <!-- Workshop2 -->
        <v-window-item key="workshop2" class="align-self-center">
          <v-card class="ma-4" :height="cardHeight" :width="cardWidth">
            <v-img
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRrpG_jyjMcYecYpTKMTrR9XSJsmj_eou82ni_HDVSq_e-AvVXeXdVqUMD26q8ngkS4aLE&usqp=CAU"
              height="300px"
            />
            <v-card-title>Workshop_02</v-card-title>
            <v-card-subtitle>Grade Cal.</v-card-subtitle>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="orange lighten-2"
                text
                @click="toggleShow('workshop2')"
                >Read More</v-btn
              >
            </v-card-actions>
            <v-expand-transition>
              <div v-show="show.workshop2">
                <v-divider></v-divider>
                <v-card-text>
                  <div class="font-weight-bold ml-8 mb-2">
                    <form @submit.prevent="submitForm">
                      <label>กรอกคะแนน</label>
                      <v-row>
                        <v-col cols="12" sm="6" md="3">
                          <v-text-field type="number" v-model.number="point"
                        /></v-col>
                        <v-col cols="12" sm="6" md="3">
                          <v-btn type="submit">คำนวน</v-btn></v-col
                        >
                      </v-row>
                    </form>
                    <p class="pt-10">เกรดที่ได้: {{ grade }}</p>
                  </div>
                </v-card-text>
              </div>
            </v-expand-transition>
          </v-card>
        </v-window-item>
      </v-window>
    </v-sheet>
    <TrainCard />
  </div>
</template>
  
  <script>
import TrainCard from "@/components/trainCard.vue";

export default {
  name: "Me",
  components: {
    TrainCard,
  },
  data() {
    return {
      model: "",
      cardWidth: "60vw", // Default width for small screens
      cardHeight: "auto", // Default height
      show: {
        info: false,
        study: false,
        others: false,
        workshop2: false,
        others_selection: 1,
      },
      point: 0,
      grade: "ยังไม่ได้คำนวน",
      messages: [
        {
          from: "Software Engineer",
          message: "Internet Thailand Public Company Limited.",
          time: "2024",
          color: "green",
        },
        {
          from: "Bachelor of Computer Engineering",
          message: "Chiang Mai University",
          time: "2020 - 2024",
          color: "purple",
        },
        {
          from: "High School",
          message: "Chongfah Xinsheng Wanich Bamrung School",
          time: "2013 - 2020",
          color: "red",
        },
      ],
    };
  },
  mounted() {
    this.updateCardSize();
    window.addEventListener("resize", this.updateCardSize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.updateCardSize);
  },
  methods: {
    updateCardSize() {
      if (window.innerWidth >= 768) {
        this.cardWidth = "40rem"; // Larger width for medium to large screens
      } else {
        this.cardWidth = "90vw"; // Smaller width for small screens
      }
    },
    toggleShow(card) {
      this.show[card] = !this.show[card];
    },
    submitForm() {
      let gradeCal = this.point;
      if (gradeCal > 100 || gradeCal < 0) {
        this.grade = "กรอกใหม่";
      } else if (gradeCal >= 80) {
        this.grade = "A";
      } else if (gradeCal >= 70) {
        this.grade = "B";
      } else if (gradeCal >= 60) {
        this.grade = "C";
      } else if (gradeCal >= 50) {
        this.grade = "D";
      } else {
        this.grade = "F";
      }
    },
  },
};
</script>
  
  <style scoped>
@media (min-width: 768px) {
  .v-card {
    width: 40rem !important;
  }
}
</style>
  