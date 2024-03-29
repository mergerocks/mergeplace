<template>
  <div class="meeting-room" v-scroll="handleScroll">
    <div class="scroll" :style="scrollStyle">
      <div class="scroll__inner">
        <div class="scroll__line"></div>
        <p class="scroll__text">scroll</p>
      </div>
    </div>
    <!-- 2 wrappers to implement dual adaptive indents -->
    <div class="meeting-room__wrapper">
      <div class="meeting-room__inner">
        <header
          class="meeting-room__header animated d06 delay-02s fadeInLeft"
          v-show="hideElements"
        >
          <h1 class="meeting-room__title">{{ $t("meetingRoom.title") }}</h1>
        </header>
        <section class="meeting-room__slider animated d06 delay-03s fadeInLeft">
          <p class="meeting-room__label-button">
            {{ $t("meetingRoom.label") }}
          </p>
          <slider v-show="hideElements"></slider>
        </section>
        <section class="meeting-room-inf" v-show="hideElements">
          <div class="meeting-room-inf__wrapper">
            <div
              class="meeting-room-inf__labels animated d06 delay-07s fadeInLeft"
            >
              <div class="beneffits__label">
                <img
                  src="../assets/image/meeting.png"
                  alt="meeting"
                  class="beneffits__image"
                />
                <p class="beneffits__text">
                  {{ $t("meetingRoom.features.meeting") }}
                </p>
              </div>
              <div class="beneffits__label">
                <img src="../assets/image/tv.svg" class="beneffits__image" />
                <p class="beneffits__text">
                  {{ $t("meetingRoom.features.tv") }}
                </p>
              </div>
              <div class="beneffits__label">
                <img
                  src="../assets/image/flipchart.svg"
                  class="beneffits__image"
                />
                <p class="beneffits__text">
                  {{ $t("meetingRoom.features.flipchart") }}
                </p>
              </div>
              <div class="beneffits__label">
                <img
                  src="../assets/image/wireless-speaker.svg"
                  class="beneffits__image"
                />
                <p class="beneffits__text">
                  {{ $t("meetingRoom.features.speaker") }}
                </p>
              </div>
            </div>
          </div>
        </section>
      </div>
    </div>
    <section
      class="next-page-nav animated d06 delay-09s fadeInLeft"
      v-show="hideElements"
    >
      <router-link
        to="/coworking"
        class="
          next-page-nav__link
          meeting-room__link-page meeting-room__link-page--interior
        "
      >
        <div class="next-page-nav__inner">
          <p class="next-page-nav__text">{{ $t("links.interior") }}</p>
        </div>
      </router-link>
    </section>
  </div>
</template>

<script>
import ButtonBookRoom from "@/components/buttons/ButtonBookRoom.vue";
import ButtonResidentLink from "@/components/buttons/ButtonResidentLink.vue";
import ButtonBookNow from "@/components/buttons/ButtonBookNow.vue";
import Slider from "@/components/Slider.vue";
import Calendar from "@/components/Calendar.vue";
import BookMeetingRoom from "@/views/BookMeetingRoom.vue";
import { mapState } from "vuex";

export default {
  name: "MeetingRoom",
  components: {
    ButtonBookRoom,
    ButtonResidentLink,
    ButtonBookNow,
    Slider,
    Calendar,
    BookMeetingRoom,
  },
  data() {
    return {
      hideElements: true,
      showBookMeetingRoom: false,
      scrollStyle: {
        transform: null,
      },
    };
  },
  methods: {
    editDate(href) {
      this.hideElements = true;
      setTimeout(() => {
        this.showBookMeetingRoom = false;
        this.toCalendar(href);
      }, 100);
    },
    showBook() {
      this.showBookMeetingRoom = true;
      setTimeout(() => {
        this.hideElements = false;
      }, 100);
    },
    goBack() {
      this.hideElements = true;
      setTimeout(() => {
        this.showBookMeetingRoom = false;
      }, 100);
    },
    toCalendar(href) {
      let top = document.getElementById(href).getBoundingClientRect().top;
      let coord = top + pageYOffset;
      window.scrollTo(0, coord - 2);
    },
    handleScroll(evt, el) {
      let currentHeight = +el.scrollHeight,
        viewportHeight = +window.innerHeight;
      if (window.innerWidth > 920) {
        viewportHeight -= 310;
      } else {
        viewportHeight -= 720;
      }
      let height = currentHeight - viewportHeight,
        posY = window.scrollY,
        percent;
      if (posY) {
        percent = Math.round(posY / (height / 80));
      } else {
        percent = 0;
      }
      let position;
      position = (viewportHeight / 100) * percent;
      this.scrollStyle.transform = `translateY(${position}px)`;
    },
  },
  computed: {
    ...mapState("meetingRoom", ["price"]),
  },
  mounted() {
    if (this.$route.path == "/meeting-room/calendar") {
      setTimeout(() => {
        this.toCalendar("fullcalendar");
      }, 350);
    }
  },
};
</script>

<style lang="scss">
.meeting-room {
  width: 100%;
  @extend %flex-col;
  align-items: center;
  justify-items: center;
  position: relative;
  padding-top: 7rem;
  @media (orientation: landscape) and (max-width: 820px) {
    padding-top: 20pt;
  }
  @media (max-width: 600px) {
    padding: 0;
  }
  &__wrapper {
    width: 100%;
    display: flex;
    padding: 0 112px;
    @media (max-width: 920px) {
      justify-content: flex-start;
      padding: 0 0 0 112px;
    }
    @media (orientation: landscape) and (max-width: 820px) {
      padding: 0 0 0 56pt;
    }
    @media (max-width: 600px) {
      justify-content: flex-start;
      padding: 0;
    }
  }
  &__inner {
    width: 100%;
    padding: 0 10%;
    @extend %flex-col-c;
    align-items: flex-start;
    &--margin {
      margin-bottom: 4rem;
    }
    @media (max-width: 960px) {
      padding: 0 5%;
    }
    @media (max-width: 600px) {
      padding: 0;
    }
  }
  .button-book-room {
    background-color: $MERGE-SECONDARY-COLOR;
    margin-top: 17px;
    &__text {
      color: $MAIN-DARK-COLOR;
    }
    &__img {
      @media (max-width: 600px) {
        display: block;
      }
    }
    &:active {
      background-color: $MERGE-DARK-COLOR;
    }
    &:active .button-book-room__text,
    &:focus .button-book-room__text {
      color: $MAIN-DARK-COLOR;
    }
    &__text::before {
      border-color: $MERGE-SECONDARY-COLOR;
    }
    &:focus &__text::before {
      visibility: visible;
    }
    @media (max-width: 600px) {
      margin: 0;
    }
  }
  &__button-book {
    display: none;
    @media (max-width: 600px) {
      width: 100%;
      display: block;
      padding: 32pt;
    }
    @media (max-width: 375px) {
      padding: 32pt 26pt;
    }
    @media (max-width: 320px) {
      padding: 32pt 22pt;
    }
  }
  &__header {
    width: 100%;
    @extend %flex-row-sb;
    align-items: center;
    justify-content: space-between;
    margin: 0 0 5rem 0;
    @media (max-width: 1200px) {
      flex-direction: column;
      align-items: flex-start;
    }
    @media (max-width: 600px) {
      order: 0;
      padding: 0 32pt;
      margin-bottom: 32pt;
    }
    @media (max-width: 375px) {
      margin-bottom: 28pt;
      padding: 0 26pt;
    }
    @media (max-width: 320px) {
      margin-bottom: 26pt;
      padding: 0 22pt;
    }
    .button-book-room {
      @media (max-width: 600px) {
        display: none;
      }
    }
  }
  &__title {
    font-family: $title-font;
    font-size: 5rem;
    font-weight: 500;
    text-align: left;
    color: $TEXT-COLOR;
    margin: 0;
    @media (max-width: 1200px) {
      margin-bottom: 2rem;
    }
    @media (max-width: 600px) {
      align-self: flex-start;
      text-align: left;
      margin: 0;
      font-size: 2.5rem;
    }
  }
  &__slider {
    @extend %flex-col;
    align-items: flex-start;
    padding-top: 5rem;
    padding-bottom: 3rem;
    width: 100%;
    @media (max-width: 600px) {
      order: 1;
      padding: 0;
    }
  }
  &__label-button {
    transition: 1.5s all cubic-bezier(0.39, 0.575, 0.565, 1);
    padding: 0.5rem 1rem;
    background-color: black;
    font-family: Montserrat;
    font-size: 0.875rem;
    font-weight: bold;
    text-align: center;
    color: $MIDDLE-GREY;
    outline: none;
    border: none;
    transition: color ease-in-out 0.2s;
    margin-bottom: 1.5rem;
    @media (max-width: 600px) {
      display: none;
    }
  }
  &__link-page {
    &--interior {
      background-image: url("../assets/image/interior.jpg");
    }
    &--events {
      background-image: url("../assets/image/events.jpg");
    }
  }
}
.meeting-room-inf {
  width: 100%;
  @extend %flex-row;
  @media (max-width: 980px) {
    margin-bottom: 4rem;
  }
  @media (max-width: 720px) {
    justify-content: center;
  }
  @media (max-width: 600px) {
    padding: 36pt 32pt 0;
    order: 2;
    border: none;
    margin: 0;
  }
  @media (max-width: 375px) {
    padding: 26pt 26pt 0;
  }
  @media (max-width: 320px) {
    padding: 22pt 22pt 0;
  }
  &__wrapper {
    flex: 0 0 65%;
    @extend %flex-col;
    @media (max-width: 720px) {
      flex: 0 0 90%;
    }
    @media (max-width: 600px) {
      border: none;
      flex-basis: 100%;
    }
  }
  &__buttons {
    padding: 5rem 0;
    width: 100%;
    border-top: 1px solid $MIDDLE-GREY-OPACITY;
    border-bottom: 1px solid $MIDDLE-GREY-OPACITY;
    @extend %flex-col;
    align-items: stretch;
    @media (max-width: 720px) {
      align-items: center;
    }
    @media (max-width: 600px) {
      padding: 0;
      order: 1;
    }
  }
  &__card {
    width: 100%;
    border-radius: 3px;
    padding: 1.875rem 2.3125rem;
    @extend %flex-row-sb;
    align-items: center;
    background: linear-gradient(100deg, #4ddfbf, #31be9e);
    margin-bottom: 2.5rem;
    @media (max-width: 720px) {
      flex-direction: column;
    }
    @media (max-width: 600px) {
      flex-direction: row;
      justify-content: stretch;
      align-items: flex-end;
      border: none;
      background: transparent;
      margin: 0;
    }
    &:last-child {
      margin: 0;
    }
    &--resident {
      border: solid 1px $MIDDLE-GREY-OPACITY;
      background: transparent;
      @media (max-width: 600px) {
        display: none;
      }
    }
    &--hour {
      @media (max-width: 600px) {
        display: none;
      }
    }
    &--hour-mobile {
      display: none;
      @media (max-width: 600px) {
        display: flex;
        padding: 10pt 0;
      }
    }
    &--resident-mobile {
      display: none;
      @media (max-width: 600px) {
        display: flex;
        padding: 0 0 10pt 0;
      }
    }

    .button-book-now,
    .button-resident-link {
      @media (max-width: 600px) {
        display: none;
      }
    }
  }
  &__text {
    @extend %flex-row;
    align-items: center;
    text-transform: uppercase;
    font-family: $title-font;
    font-size: 1.875rem;
    font-weight: 500;
    text-align: left;
    color: $MAIN-DARK-COLOR;
    line-height: 1;
    margin-right: 0.625rem;
    @media (max-width: 720px) {
      margin-right: 0;
      margin-bottom: 1rem;
    }
    @media (max-width: 600px) {
      font-size: 2.4rem;
      flex: 0 0 50%;
      margin: 0;
    }
    @media (max-width: 375px) {
      font-size: 2.2rem;
    }
    @media (max-width: 320px) {
      flex: 0 0 45%;
      font-size: 1.85rem;
    }
    &--hour {
      align-items: baseline;
      @media (max-width: 600px) {
        color: $TEXT-COLOR;
        white-space: nowrap;
        display: flex;
        flex-flow: row nowrap;
      }
    }
    &--resident {
      color: $GREY;
    }
  }
  &__description {
    padding-top: 4px;
    text-transform: uppercase;
    font-family: $base-font;
    font-size: 0.625rem;
    font-weight: bold;
    line-height: 1.4;
    letter-spacing: 0.7px;
    text-align: left;
    color: $DARK-GREY;
    padding-left: 0.625rem;
    white-space: normal;
    @media (max-width: 720px) {
      min-width: 0;
    }
    @media (max-width: 600px) {
      padding: 0;
      flex: 0 0 50%;
      font-size: 0.7rem;
    }
    @media (max-width: 375px) {
      font-size: 0.65rem;
    }
    @media (max-width: 320px) {
      flex: 0 0 55%;
      font-size: 0.6rem;
    }
    &--resident {
      color: $GREY;
      width: 220px;
      @media (max-width: 600px) {
        width: 100%;
        flex: 100%;
      }
    }
    &--hour {
      @media (max-width: 600px) {
        color: $TEXT-COLOR;
        font-size: 0.9rem;
        font-weight: 500;
      }
      @media (max-width: 375px) {
        font-size: 0.8rem;
      }
      @media (max-width: 320px) {
        font-size: 0.7rem;
      }
    }
    &--currency {
      padding-left: 15px;
      @media (max-width: 375px) {
        padding-left: 7px;
      }
    }
  }
  &__labels {
    width: 100%;
    padding: 5rem 0;
    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-template-rows: repeat(2, auto);
    grid-gap: 3.75rem;
    @media (max-width: 600px) {
      padding: 0;
      grid-template-columns: repeat(2, 47.5%);
      grid-column-gap: 5%;
      grid-row-gap: 32pt;
      order: 0;
      margin-bottom: 32pt;
    }
  }
}
</style>
