<template>
  <section id="hello" class="hello">
    <div class="hello__title-wrapper">
      <h1 class="hello__title">
        <span class="hello__title hello__title--nowrap">
          <vue-typer
            :text="$t('hello.title.0')"
            :repeat="0"
            :shuffle="false"
            initial-action="typing"
            :pre-type-delay="700"
            :type-delay="200"
            :erase-on-complete="false"
            caret-animation="smooth"
            @typed="activeString = 1"
          ></vue-typer>
        </span>
        <span class="hello__title hello__title--nowrap">
          <vue-typer
            :text="$t('hello.title.1')"
            :repeat="0"
            :shuffle="false"
            initial-action="typing"
            :pre-type-delay="700"
            :type-delay="200"
            :erase-on-complete="false"
            caret-animation="smooth"
            v-if="activeString >= 1"
            @typed="activeString = 2"
          ></vue-typer>
        </span>
      </h1>
      <h1 class="hello__title hello__title--second">
        <span class="hello__title hello__title--nowrap hello__logo">
          <vue-typer
            :text="$t('hello.title.2')"
            :repeat="0"
            :shuffle="false"
            initial-action="typing"
            :pre-type-delay="700"
            :type-delay="200"
            :erase-on-complete="false"
            caret-animation="smooth"
            v-if="activeString >= 2"
            @typed="activeString = 3"
          ></vue-typer>
        </span>
        <span class="hello__title hello__title--nowrap hello__logo">
          <vue-typer
            :text="$t('hello.title.3')"
            :repeat="0"
            :shuffle="false"
            initial-action="typing"
            :pre-type-delay="700"
            :type-delay="200"
            :erase-on-complete="false"
            caret-animation="smooth"
            v-if="activeString >= 3"
          ></vue-typer>
        </span>
      </h1>
    </div>
    <h2 class="hello__subtitle animated d05 delay-02s fadeInLeft">
      {{ $t("hello.subtitle") }}
    </h2>
    <div class="hello-link__wrapper animated d06 delay-03s fadeInLeft">
      <a
        :href="$t('hello.link.wayUrl')"
        target="_blank"
        class="hello-link hello-link--how-get"
      >
        <svg class="hello-link__img">
          <use xlink:href="#videocamera" />
        </svg>
        <p class="hello-link__text">{{ $t("hello.link.way") }}</p>
      </a>
      <router-link to="/about" class="hello-link hello-link--prices">
        <svg class="hello-link__img">
          <use xlink:href="#infoborder" />
        </svg>
        <p class="hello-link__text">{{ $t("hello.link.info") }}</p>
      </router-link>
    </div>
    <p class="hello__text animated d05 delay-04s fadeInLeft">
      {{ $t("hello.text.clean_0") }}
      <router-link to="/coworking" class="hello__text--link">{{
        $t("hello.text.link_0")
      }}</router-link>
      {{ $t("hello.text.clean_1") }}
      <a
        href="https://www.facebook.com/merge.place/"
        target="_blank"
        class="hello__text--link"
        >{{ $t("hello.text.link_1") }}</a
      >
      {{ $t("hello.text.clean_2") }}
      <router-link to="/meeting-room" class="hello__text--link">{{
        $t("hello.text.link_2")
      }}</router-link>
      {{ $t("hello.text.clean_3") }}
      {{ $t("hello.text.link_3") }}
      {{ $t("hello.text.clean_4") }}
    </p>
    <div class="hello__button-wrapper animated d05 delay-05s fadeInLeft">
      <button-membership
        class="hello__button"
        @click.native="becomeMember"
      ></button-membership>
      <button-book-room
        class="hello__button"
        @click.native="meetingRoom"
      ></button-book-room>
    </div>
    <svg style="display: none">
      <symbol id="videocamera" viewBox="0 0 24 24">
        <path
          d="M17,10.5 L17,7 C17,6.45 16.55,6 16,6 L4,6 C3.45,6 3,6.45 3,7 L3,17 C3,17.55 3.45,18 4,18 L16,18 C16.55,18 17,17.55 17,17 L17,13.5 L21,17.5 L21,6.5 L17,10.5 L17,10.5 Z"
          id="Shape"
        ></path>
      </symbol>
      <symbol id="infoborder" viewBox="0 0 24 24">
        <path
          d="M11,17 L13,17 L13,11 L11,11 L11,17 L11,17 Z M12,2 C6.48,2 2,6.48 2,12 C2,17.52 6.48,22 12,22 C17.52,22 22,17.52 22,12 C22,6.48 17.52,2 12,2 L12,2 Z M12,20 C7.59,20 4,16.41 4,12 C4,7.59 7.59,4 12,4 C16.41,4 20,7.59 20,12 C20,16.41 16.41,20 12,20 L12,20 Z M11,9 L13,9 L13,7 L11,7 L11,9 L11,9 Z"
          id="Shape"
        ></path>
      </symbol>
    </svg>
  </section>
</template>

<script>
import { VueTyper } from "vue-typer";
import ButtonMembership from "@/components/buttons/ButtonMembership.vue";
import ButtonBookRoom from "@/components/buttons/ButtonBookRoom.vue";

export default {
  name: "Hello",
  components: {
    ButtonMembership,
    ButtonBookRoom,
    VueTyper,
  },
  data() {
    return {
      activeString: 0,
    };
  },
  methods: {
    meetingRoom() {
      this.$router.push("/meeting-room");
    },
    becomeMember() {
      this.$router.push("/about");
    },
  },
};
</script>

<style lang="scss">
.hello {
  padding: 3rem 3rem 3rem 112px;
  width: 100%;
  grid-column: 2;
  display: grid;
  grid-template-columns: 10% auto auto;
  grid-template-rows: repeat(5, auto);
  grid-template-areas:
    ". title    "
    ". subtitle "
    ". link     "
    ". text     "
    ". btn      ";
  grid-row-gap: 2rem;
  align-content: center;
  justify-items: start;
  justify-content: start;
  @media (max-width: 600px) {
    grid-row-gap: 0rem;
    grid-template-columns: 5% auto auto;
    padding: 1rem 1rem 1rem 112px;
  }
  @media (orientation: landscape) and (max-width: 820px) {
    grid-template-columns: 5% auto auto;
    padding: 0 0 0 56pt;
  }
  @media (max-width: 600px) {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: flex-start;
    padding: 0 32pt 32pt;
    flex: 1 0 100%;
  }
  @media (max-width: 375px) {
    padding: 0 26pt 26pt;
  }
  @media (max-width: 320px) {
    padding: 0 22pt 22pt;
  }
  &__title {
    @extend %flex-row;
    align-items: center;
    justify-content: flex-start;
    margin: 0;
    font-size: 5rem;
    text-align: left;
    font-family: $title-font;
    color: $TEXT-COLOR;
    font-weight: 500;
    flex-wrap: wrap;
    .vue-typer {
      font-family: $title-font;
      font-weight: 500;
      .custom.char {
        color: $TEXT-COLOR;
      }
      .custom.caret {
        background-color: $TEXT-COLOR;
      }
    }
    @media (max-width: 1024px) {
      font-size: 3rem;
    }
    @media (max-width: 600px) {
      text-align: left;
      font-size: 2.6rem;
    }
    @media (max-width: 540px) {
      font-size: 2rem;
      line-height: 1.2;
    }
    @media (max-width: 320px) {
      font-size: 1.6rem;
    }
    &--nowrap {
      flex-direction: row;
      align-items: center;
      flex-wrap: nowrap;
      white-space: nowrap;
    }
  }
  &__title-wrapper {
    @extend %flex-col;
    grid-area: title;
    @media (max-width: 600px) {
      margin-bottom: 28pt;
    }
    @media (max-width: 500px) {
      margin-bottom: 24pt;
    }
    @media (max-width: 375px) {
      margin-bottom: 16pt;
    }
    @media (max-width: 320px) {
      margin-bottom: 10pt;
    }
  }
  &__title-wrap {
    display: none;
    @media (max-width: 840px) {
      display: block;
    }
  }
  &__logo {
    color: $MERGE-MAIN-COLOR;
    .vue-typer {
      .custom.char {
        color: $MERGE-MAIN-COLOR;
      }
      .custom.caret {
        background-color: $TEXT-COLOR;
      }
    }
  }
  &__subtitle {
    margin: 0;
    grid-area: subtitle;
    text-transform: uppercase;
    font-family: $base-font;
    color: white;
    font-size: 1.1rem;
    font-weight: 700;
    white-space: nowrap;
    @media (max-width: 600px) {
      font-size: 0.8rem;
      line-height: 2;
      font-weight: 600;
      letter-spacing: 0.8pt;
      white-space: normal;
    }
    @media (max-width: 320px) {
      font-size: 0.7rem;
    }
  }
  &__text {
    max-width: 45%;
    min-width: 553px;
    grid-area: text;
    align-items: start;
    font-family: $base-font;
    color: white;
    font-size: 13px;
    font-weight: 500;
    text-align: left;
    line-height: 2.5;
    border-top: 1px solid $BUTTON-COLOR;
    padding: 1.8rem 0 1.2rem 0;
    @media (max-width: 810px) {
      min-width: fit-content;
      width: 100%;
    }
    @media (max-width: 600px) {
      padding: 2rem 0;
      border: none;
      display: none;
    }
    &--link {
      text-decoration: none;
      color: $TEXT-LINK-COLOR;
      font-weight: 600;
    }
  }
  &__button-wrapper {
    @extend %flex-row;
    grid-area: btn;
    @media (max-width: 600px) {
      flex-direction: column;
      width: 100%;
      flex: 1 0 100%;
      justify-content: flex-start;
    }
  }
  &__button {
    &:first-child {
      margin-right: 2rem;
      @media (max-width: 600px) {
        margin: 0 0 16pt;
      }
    }
    @media (max-width: 540px) {
      width: 100%;
    }
  }
}

.hello-link {
  text-decoration: none;
  display: grid;
  grid-template-columns: repeat(2, auto);
  justify-items: start;
  align-items: center;
  grid-column-gap: 0.6rem;
  border-radius: 3px;
  border: solid 2.5px transparent;
  padding: 4px 6px;
  transition: border-color ease-in-out 0.1s;
  @media (max-width: 600px) {
    grid-column-gap: 9pt;
    width: 100%;
    justify-content: start;
    &:first-child {
      margin-bottom: 14pt;
    }
  }
  @media (max-width: 375px) {
    &:first-child {
      margin-bottom: 10pt;
    }
  }
  @media (max-width: 320px) {
    &:first-child {
      margin-bottom: 6pt;
    }
  }
  @media (min-width: 600px) {
    &:hover .hello-link__text,
    &:hover .hello-link__img {
      color: $MERGE-MAIN-COLOR;
      fill: $MERGE-MAIN-COLOR;
    }
  }
  &:focus {
    border: solid 2.5px rgba(55, 205, 171, 0.5);
  }
  &:active .hello-link__text,
  &:active .hello-link__img {
    color: $MERGE-DARK-COLOR;
    fill: $MERGE-DARK-COLOR;
  }
  &__wrapper {
    justify-self: start;
    position: relative;
    left: -10px;
    grid-area: link;
    @extend %flex-row;
    a:first-child {
      margin-right: 2rem;
    }
    @media (max-width: 600px) {
      flex-direction: column;
      align-items: flex-start;
      padding: 26pt 0 36pt;
    }
    @media (max-width: 375px) {
      padding: 22pt 0 32pt;
    }
    @media (max-width: 320px) {
      padding: 14pt 0 22pt;
    }
  }

  &__img {
    width: 16px;
    height: 16px;
    fill: $MERGE-SECONDARY-COLOR;
    transition: fill ease-in-out 0.1s;
    @media (max-width: 600px) {
      width: 16pt;
      height: 16pt;
    }
  }

  &__text {
    text-transform: uppercase;
    font-size: 10px;
    font-family: $base-font;
    color: $MERGE-SECONDARY-COLOR;
    font-weight: 700;
    white-space: nowrap;
    transition: color ease-in-out 0.1s;
    @media (max-width: 600px) {
      font-size: 0.8rem;
      letter-spacing: 0.7pt;
    }
    @media (max-width: 320px) {
      font-size: 0.6rem;
      letter-spacing: 0.5pt;
    }
  }

  &--how-get {
    grid-area: link-1;
  }

  &--prices {
    grid-area: link-2;
  }
}
</style>
