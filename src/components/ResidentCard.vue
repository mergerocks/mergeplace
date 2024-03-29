<template>
  <div class="resident-card__wrapper-all" @click.self="close">
    <div class="resident-card__wrapper" @click.self="close">
      <div class="resident-card animated faster fadeInBubble">
        <button-close-mini
          class="resident-card__close"
          @click.native="close"
        ></button-close-mini>
        <div class="resident-card__inner resident-card__inner--top">
          <p class="resident-card__title">{{ $t("residentCard.title") }}</p>
          <p class="resident-card__description">
            {{ $t("residentCard.description") }}
          </p>
          <div class="resident-card__label resident-card__label--room">
            <img
              src="../assets/image/meeting-room.svg"
              alt="meeting room"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.meetingRoom") }}
            </p>
          </div>
          <div class="resident-card__label resident-card__label--lecture">
            <img
              src="../assets/image/lectures.svg"
              alt="lectures"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.lectures") }}
            </p>
          </div>
        </div>
        <div class="resident-card__line"></div>
        <div class="resident-card__inner resident-card__inner--middle">
          <div class="resident-card__label">
            <img
              src="../assets/image/wi-fi.svg"
              alt="wi-fi"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.wifi") }}
            </p>
          </div>
          <div class="resident-card__label">
            <img
              src="../assets/image/unlimited-coffee-tea.svg"
              alt="coffe"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.coffee") }}
            </p>
          </div>
          <div class="resident-card__label">
            <img
              src="../assets/image/printer.svg"
              alt="printer"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.printer") }}
            </p>
          </div>
          <div class="resident-card__label">
            <img
              src="../assets/image/shower.svg"
              alt="shower"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.shower") }}
            </p>
          </div>
          <div class="resident-card__label">
            <img
              src="../assets/image/microwave.svg"
              alt="kitchen"
              class="resident-card__image"
            />
            <p class="resident-card__text">
              {{ $t("residentCard.features.kitchen") }}
            </p>
          </div>
        </div>
        <div class="resident-card__inner resident-card__inner--price">
          <p class="resident-card__price">
            {{ $t("dayCard.price") }}
            <span class="resident-card__sum"
              >{{ $t("prices.month")
              }}<span class="resident-card__sum-currency">
                {{ $t("currency") }}
              </span>
            </span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ButtonCloseMini from "@/components/buttons/ButtonCloseMini.vue";
import ButtonResident from "@/components/buttons/ButtonResident.vue";
import { mapMutations } from "vuex";

export default {
  name: "ResidentCard",
  components: {
    ButtonCloseMini,
    ButtonResident,
  },
  methods: {
    ...mapMutations("workplace", ["setTariff"]),
    close() {
      this.$emit("closeCard");
    },
    becomeResident() {
      this.setTariff("month");
      this.$emit("closeCard", "month");
    },
  }
};
</script>

<style lang="scss">
.resident-card {
  padding: 2rem 2.4rem 3.5rem 2.4rem;
  flex: 0 0 36%;
  border-radius: 3px;
  background-color: $BUTTON-COLOR;
  box-shadow: 0 12px 30px 24px rgba(0, 0, 0, 0.1);
  @extend %flex-col;
  align-items: stretch;
  position: relative;
  @media (min-width: 600px) {
    min-width: 520px;
  }
  @media (max-width: 600px) {
    padding: 20pt 24pt;
    flex: 0 0 100%;
    align-self: flex-start;
  }
  @media (max-width: 320px) {
    padding: 16pt 18pt;
  }
  &__wrapper {
    padding: 2rem;
    top: 0;
    left: 0;
    right: 0;
    width: 100%;
    min-height: 100vh;
    background-color: transparent;
    @extend %flex-row-c;
    align-items: center;
    position: fixed;
    z-index: 100;
    will-change: opacity;
    @media (max-height: 800px) {
      position: absolute;
    }
    @media (max-width: 600px) {
      padding: 54pt 20pt;
      align-items: flex-start;
    }
    @media (max-width: 375px) {
      padding: 34pt 20pt;
    }
    @media (max-width: 320px) {
      padding: 24pt 20pt;
    }
  }
  &__wrapper-all {
    position: absolute;
    z-index: 99;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    min-height: 100vh;
    background-color: rgba(17, 17, 17, 0.7);
  }
  &__close {
    @media (max-width: 600px) {
      svg {
        width: 20pt;
        height: 20pt;
      }
      top: 28pt;
    }
    @media (max-width: 320px) {
      top: 22pt;
    }
  }
  &__button {
    align-self: center;
    @media (max-width: 600px) {
      display: none;
    }
  }
  &__title {
    font-family: $title-font;
    font-size: 1.5rem;
    font-weight: 500;
    text-align: left;
    color: $TEXT-COLOR;
    grid-area: 1 / 1 / 2 / 3;
    @media (max-width: 600px) {
      font-size: 1.5rem;
      line-height: 2;
      letter-spacing: 0.5pt;
    }
    @media (max-width: 320px) {
      font-size: 1.3rem;
      letter-spacing: 0.3pt;
    }
  }
  &__description {
    padding: 0.3125rem 0 1.9375rem 0;
    font-family: $base-font;
    font-size: 0.8125rem;
    font-weight: 500;
    line-height: 2;
    text-align: left;
    color: $GREY;
    grid-area: 2 / 1 / 3 / 3;
    @media (max-width: 600px) {
      font-size: 0.8rem;
      padding: 0;
      margin-bottom: 22pt;
      letter-spacing: 0.5pt;
    }
    @media (max-width: 320px) {
      margin-bottom: 12pt;
    }
  }
  &__line {
    width: 100%;
    height: 1px;
    background-color: $DARK-GREY-OPACITY;
    margin: 2rem 0;
    @media (max-width: 600px) {
      margin: 14pt 0;
    }
  }
  &__inner {
    display: grid;
    align-items: center;
    @media (max-width: 600px) {
      display: flex;
      flex-direction: column;
      align-items: flex-start;
    }
    &--top {
      grid-template-columns: repeat(2, 1fr);
      grid-template-rows: repeat(3, auto);
      grid-column-gap: 2rem;
    }
    &--middle {
      grid-template-columns: repeat(2, 1fr);
      grid-template-rows: repeat(3, auto);
      grid-row-gap: 1.5rem;
      grid-column-gap: 2rem;
      margin-bottom: 2.625rem;
      @media (max-width: 600px) {
        margin: 0;
      }
    }
    &--price {
      grid-template-rows: repeat(2, auto);
      grid-row-gap: 1.5rem;
      justify-content: center;
      justify-items: center;
      @media (max-width: 600px) {
        display: none;
      }
    }
  }
  &__label {
    display: grid;
    grid-template-columns: repeat(2, auto);
    grid-column-gap: 1rem;
    align-items: center;
    justify-content: start;
    @media (max-width: 600px) {
      margin-bottom: 18pt;
      &:last-child {
        margin: 0;
      }
    }
    @media (max-width: 320px) {
      margin-bottom: 12pt;
    }
    &--room {
      grid-area: 3 / 1 / 4 / 2;
      @media (max-width: 600px) {
        margin-bottom: 20pt;
      }
      @media (max-width: 320px) {
        margin-bottom: 12pt;
      }
    }
    &--lecture {
      grid-area: 3 / 2 / 4 / 3;
      @media (max-width: 600px) {
        margin: 0;
      }
    }
  }
  &__image {
    width: 32px;
    height: 32px;
    fill: $MERGE-MAIN-COLOR;
    @media (max-width: 600px) {
      width: 24pt;
      height: 24pt;
    }
  }
  &__text {
    font-family: $base-font;
    font-size: 0.625rem;
    font-weight: 500;
    line-height: 1.6;
    text-align: left;
    color: $TEXT-COLOR;
    @media (max-width: 600px) {
      font-size: 0.8rem;
    }
    @media (max-width: 320px) {
      font-size: 0.7rem;
      font-weight: 500;
    }
  }
  &__price {
    font-family: $base-font;
    font-size: 0.8125rem;
    font-weight: 500;
    line-height: 1;
    text-align: center;
    color: white;
  }
  &__sum {
    font-family: $title-font;
    font-size: 1.875rem;
    font-weight: 700;
    text-align: left;
    color: white;
  }
  &__sum-currency {
    text-transform: uppercase;
    font-family: $base-font;
    font-size: 0.5rem;
    font-weight: 700;
    line-height: 2;
    letter-spacing: 0.5px;
    text-align: left;
    color: $GREY;
  }
}
</style>
