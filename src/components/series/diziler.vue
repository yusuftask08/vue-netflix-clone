<template>
  <div class="populer-diziler">
    <div class="text-span">
      <span>Popüler Diziler</span>
    </div>

    <swiper
      :slides-per-view="7"
      :space-between="50"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
      :mousewheel-control="false"
      :performance-mode="false"
      :pagination-visible="true"
      :pagination-clickable="false"
      :autoScrollOffset="0"
      :draggable="false"
      :mousewheel="false"
      class="item ms-5 swiper-scrollbar-lock"
    >
      <swiper-slide
        v-for="popularList in seriesPopularList"
        :key="popularList.id"
      >
        <div class="ms-2 me-2 movie_card item">
          <img
            :src="'http://image.tmdb.org/t/p/w500/' + popularList.poster_path"
            class="card-img-top"
            alt="..."
          />
          <div class="film_info" v-if="isAuthenticated">
            <div class="list-icon-left">
              <a
                ><i class="fas fa-play" style="background: white; color: black">
                </i
              ></a>

              <a @click="addFavorite(popularList)"
                ><i class="fas fa-plus toolTip">
                  <span class="toolTiptext-sm tool-span-sm">
                    Listeme ekle
                  </span>
                </i></a
              >
              <a
                ><i class="fas fa-chevron-down toolTip">
                  <span class="toolTiptext-sm tool-span-sm">
                    Daha fazla bilgi
                  </span>
                </i></a
              >
            </div>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";
import SwiperCore, { Navigation, Pagination, A11y } from "swiper";

// Import Swiper styles
import "swiper/components/navigation/navigation.scss";
import "swiper/swiper.scss";
import axios from "axios";
import modals from "@/components/modal/modals";
import { mapGetters } from "vuex";

SwiperCore.use([Navigation, Pagination, A11y]);
export default {
  components: {
    Swiper,
    SwiperSlide,
    Navigation,
    modals,
  },
  data() {
    return {
      seriesPopularList: [],
      isOpen: false,
    };
  },
  methods: {
    addFavorite(popularList) {
      axios
        .post("http://localhost:3000/favorites", {
          ...popularList,
          isFavorite: true,
        })
        .then((response) => {
          console.log(response);
        })
        .catch((err) => console.log(err));
    },
    showDetail(popularList) {
      console.log("populardatacek ", popularList);
      this.isOpen = !this.isOpen;
      this.modalId = popularList.id;
      this.modalData = popularList;
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${popularList.id}?api_key=7b97ca5600ae944d697e04e778928d05&language=en-US&append_to_response=videos`
        )
        .then((response) => {
          console.log("iddetailvideos", response);
          this.popularList = response.data.results;
          this.modalId.data.cast = cast;
        });
      let cast;
      for (i = 0; i < 6; i++) {
        array.push(cast[i]);
      }
    },
    onSwiper(swiper) {
      console.log(swiper);
    },
    onSlideChange() {
      console.log("slide change");
    },
  },
  created() {
    axios
      .get(
        "https://api.themoviedb.org/3/tv/popular?api_key=<//APIKEY\\>&language=en-US&page=1"
      )
      .then((response) => {
        console.log("seriesPopularList", response);
        this.seriesPopularList = response.data.results;
      });
  },
  computed: {
    ...mapGetters({
      isAuthenticated: "users/isAuthenticated",
    }),
  },
};
</script>