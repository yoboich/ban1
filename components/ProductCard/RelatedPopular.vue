<script setup>
import { useWindowSize } from '@vueuse/core';
const isLarge = ref(true);

const { width } = useWindowSize();
watchEffect(() => {
  if (width.value <= 768) {
    isLarge.value = false;
  } else {
    isLarge.value = true;
  }
});
onMounted(() => {
  if (width.value <= 768) {
    isLarge.value = false;
  }
});

defineProps(['type', 'name', 'img', 'metro', 'walk', 'price']);
</script>

<template>
  <div class="card-related__column">
    <div
        class="card-related__item"
        :class="{
				nohover: !isLarge,
			}"
    >
      <div class="card-related__img">
        <img :src="img" alt="" />
        <div class="card-related__play">
        </div>
        <nuxt-link to="/product/vip" class="btn btn-white card-related__btn"
        >Подробнее</nuxt-link
        >
      </div>
      <div class="card-related__hover">
        <div class="card-related__name h3">{{ name }}</div>
        <div class="card-related__price h3">{{ price }} руб.</div>
      </div>
      <div class="card-related__top">
        <img src="~/assets/img/icon/price.png" alt="price">
        <div class="card-related__what h4">{{ type }}</div>
        <div class="card-related__name h3">{{ name }}</div>
      </div>
      <div class="card-related__bottom">
        <div class="card-related__metro">
          <div class="card-related__metro-text h4">
            <img src="~/assets/img/icon/metro.svg" alt="" />
            {{ metro }}
          </div>
          <div class="card-related__walk">{{ walk }}</div>
        </div>
        <div class="card-related__price h3">{{ price }}</div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.card-related {
  &__row {
  }
  &__column {
    display: flex;
    align-items: stretch;
    flex: 1;
    margin: 0 21px 0 0;
    @media screen and (max-width: 768px) {
      flex: 0 1 50%;
    }
  }

  &__btn {
    display: none;
  }

  &__item {
    display: flex;
    flex-direction: column;
    border-radius: 23px;
    background: $default-color;
    padding: 1rem 0 1.9rem 0;
    transition: transform 0.3s ease-in;
    position: relative;

    @media screen and (max-width: 768px) {
      width: 100%;
    }
    &:not(.nohover):hover {
      background: #ffffff;
      box-shadow: 0px 6px 56px rgba(123, 129, 148, 0.48);
      transform: scale(1.2);
      z-index: 2;
      position: absolute;
      transition: transform 0.2s ease-in;
      padding: 0;
      display: flex;
      flex-direction: column;
      margin-left: -5%;
      .card-related__action {
        display: none;
      }
      .card-related__metro {
        display: none;
      }

      .card-related__what {
        display: none;
      }
      .card-related__bottom {
        display: none;
      }
      .card-related__top {
        display: none;
      }

      .card-related__hover {
        display: flex;
        justify-content: flex-end;
        flex-direction: row-reverse;
        gap: 2rem;
        font-size: 1.6rem;
        padding: 0 0 3.2rem 3.8rem;
      }

      .card-related__img {
        width: 38rem;
        margin: 0 0 3.8rem;
        flex: 1;
        border: 8px solid #ffffff;
        filter: drop-shadow(0px 6px 32px rgba(123, 129, 148, 0.4));
        border-radius: 15px;
        & img {
          max-height: 25.9rem;
        }
      }
      .card-related__name {
        margin: 0;
      }
      .card-related__btn {
        display: block;
        visibility: visible;
        position: absolute;
        bottom: 1.7rem;
        right: 1.7rem;
      }
    }
  }

  &__action {
    display: flex;
    align-items: center;
    margin-bottom: 1.8rem;
  }

  &__feedback {
    flex: 1;
    display: flex;
    align-items: center;
    font-weight: 500;
    font-size: 1rem;
    color: #9da7c7;
    margin-left: 0.8rem;
  }

  &__img {
    position: relative;
    margin-bottom: 1.8rem;
    width: 100%;
    margin-left: 0;

    @media screen and (max-width: 768px) {
      width: 100%;
      margin-left: 0;
    }
    & img {
      width: 100%;
      max-height: 20.9rem;
      height: 100%;
      object-fit: cover;
      filter: drop-shadow(1px 7px 22px rgba(166, 175, 205, 0.58));
      border-radius: 6px;

      @media screen and (max-width: 768px) {
        max-height: 100%;
      }
    }
  }

  &__like {
    width: 2.2rem;
  }

  &__play {
    position: absolute;
    top: 1.4rem;
    right: 1.6rem;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: rgba($color: #000000, $alpha: 0.4);
    width: 3rem;
    height: 3rem;
    border-radius: 50%;
    cursor: pointer;
    &::before {
      content: '';
      width: 1rem;
      height: 1.2rem;
      position: absolute;
      left: 36%;
      top: 31%;
      background-image: url(@/assets/img/product-card/icon.svg);
      background-size: cover;
      background-repeat: no-repeat;
      transition: all 0.2s;
    }
  }

  &__hover {
    display: none;
  }

  &__what {
    margin-bottom: 0.5rem;
    color: $secondary-color;
  }

  &__name {
    flex: 1 auto;
    margin-bottom: 1.5rem;
    color: $mainFontColor;
  }
  &__bottom {
    display: flex;
    flex-direction: column;
    margin-top: 0;
  }
  &__metro {
    display: flex;
    align-items: flex-end;
    gap: 1.3rem;
    margin-bottom: 1.5rem;
    color: $mainFontColor;

    @media screen and (max-width: 768px) {
      display: none;
    }
  }

  &__metro-text {
    display: flex;
    align-items: center;
    gap: 0.5rem;
    color: #3E3E51;
    font-family: 'Lato', sans-serif;
    font-weight: 500;
    font-size: 14px;
  }

  &__walk {
    font-family: 'Lato', sans-serif;
    font-weight: 600;
    font-size: 12px;
    color: #8F99BA;
  }

  &__price {
    font-weight: 700;
    font-family: 'Lato', sans-serif;
    font-size: 22px;
    color: #3E3E51;
  }
}
</style>
