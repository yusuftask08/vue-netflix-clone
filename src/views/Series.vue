<template>
  <div>
    <navBar />
    <backgroundSeries />
    <diziler />
    <dayPopularTv />
    <onerilenDiziler />
    <onerilenBreaking />
    <netflix />
    <footers />
  </div>
</template>
<script>
import diziler from "@/components/series/diziler";
import backgroundSeries from "@/components/series/backgroundSeries";
import dayPopularTv from "@/components/NewPopular/dayPopularTv";
import onerilenDiziler from "@/components/series/onerilenDiziler";
import onerilenBreaking from "@/components/series/onerilenBreaking";
import netflix from "@/components/series/netflix";
import footers from "@/components/footer/footers.vue";

export default {
  components: {
    diziler,
    backgroundSeries,
    dayPopularTv,
    onerilenDiziler,
    onerilenBreaking,
    netflix,
    footers,
  },
};
</script>
