<template>
    <div class="container mb-40">
      <div class="flex items-center justify-center">
        <div
          @click="openVideo()"
          class="cursor-pointer ring-1 ring-white/30 bg-cover hover:ring-white/60 relative aspect-video rounded-md shadow-white bg-black/70 group"
          :style="{
            backgroundImage: `url(${poster})`,
            width: '525px',
            height: '325px',
          }"
        >
          <div
            class="bg-white items-center justify-center px-4 flex gap-2.5 absolute group-hover:-mt-6 transition-all font-semibold leading-10 text-black/80 rounded-full top-1/2 left-1/2 w-[9rem] ml-[-4.5rem] h-10 -mt-5"
          >
            <svg
              class="h-5 w-5"
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
              fill="currentColor"
            >
              <path stroke="none" d="M0 0h24v24H0z" fill="none" />
              <path
                d="M6 4v16a1 1 0 0 0 1.524 .852l13 -8a1 1 0 0 0 0 -1.704l-13 -8a1 1 0 0 0 -1.524 .852z"
              />
            </svg>
            Ver demo
          </div>
        </div>
      </div>
      <ClientOnly>
        <ModalVideo />
      </ClientOnly>
    </div>
  </template>
  
  <script>
  import PosterImage from "~/assets/demo-v3-poster.jpg";
  export default {
    data() {
      return {
        // Define any required data here
        poster: PosterImage,
      };
    },
    methods: {
      openVideo() {
        this.$store.commit("changeVideoState", true);
        // Tracks the `login` event
        useTrackEvent("video_click", {
          reason: this.referalCode,
        });
      },
    },
    computed: {
      referalCode() {
        // Retrieve the referral code from the query parameters
        return this.$route.params.referal;
      },
      extraData() {
        if (this.$route.query) {
          //extract keys and values from object
          let values = Object.entries(this.$route.query).map(
            ([key, value]) => key + ": " + value
          );
          return values.join("; ");
        } else {
          return "";
        }
      },
    },
  };
  </script>
  