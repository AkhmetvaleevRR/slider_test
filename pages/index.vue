<template>
  <div class="slider">
    <swiper-container
      :slides-per-view="slidesPerView"
      ref="containerRef"
      space-between="20"
      @swiper="onSwiper"
      class="slider__container"
    >
      <swiper-slide
        v-for="(slide, idx) in slides"
        :key="idx"
        class="slider__slide"
      >
        <Card
          :image="slide.image"
          :tag="slide.tag"
          :description="slide.description"
          :date="slide.date"
        />
      </swiper-slide>
    </swiper-container>

    <div class="slider__controls" v-show="!isMobile">
      <button
        class="slider__button slider__button--prev"
        @click="swiper.prev()"
        :disabled="isPrevDisabled"
        aria-label="Предыдущий слайд"
      >
        <img src="~/assets/icons/Arrow.svg" alt="" class="slider__icon" />
      </button>
      <button
        class="slider__button slider__button--next"
        @click="swiper.next()"
        :disabled="isNextDisabled"
        aria-label="Следующий слайд"
      >
        <img src="~/assets/icons/Arrow.svg" alt="" class="slider__icon" />
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from "vue";

const containerRef = ref(null);
const swiper = useSwiper(containerRef);
const slidesPerView = ref(3);
const isMobile = ref(false);

const updateSlidesPerView = () => {
  const width = window.innerWidth;
  isMobile.value = width < 1200;
  if (width < 768) {
    slidesPerView.value = 1;
  } else if (width < 1200) {
    slidesPerView.value = 2;
  } else {
    slidesPerView.value = 3;
  }
};

const isPrevDisabled = computed(() => {
  return swiper.isBeginning.value;
});

const isNextDisabled = computed(() => {
  return swiper.isEnd.value;
});

const slides = [
  {
    tag: "Продукт 1",
    image: "https://placebear.com/300/200",
    description: "Описание продукта 1",
    date: "12.02.2025",
  },
  {
    tag: "Продукт 2",
    image: "https://placebear.com/300/200",
    description: "Описание продукта 2",
    date: "12.02.2025",
  },
  {
    tag: "Продукт 3",
    image: "https://placebear.com/300/200",
    description: "Описание продукта 3",
    date: "12.02.2025",
  },
  {
    tag: "Продукт 4",
    image: "https://placebear.com/300/200",
    description: "Описание продукта 4",
    date: "12.02.2025",
  },
  {
    tag: "Продукт 5",
    image: "https://placebear.com/300/200",
    description: "Описание продукта 5",
    date: "12.02.2025",
  },
];

onMounted(() => {
  updateSlidesPerView();
  window.addEventListener("resize", updateSlidesPerView);
});

onUnmounted(() => {
  window.removeEventListener("resize", updateSlidesPerView);
});
</script>

<style scoped lang="scss">
.slider {
  margin: 0 auto;
  position: relative;
  width: clamp(300px, 90%, 1500px);

  &__container {
    width: 100%;
  }

  &__slide {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  &__controls {
    position: absolute;
    top: 50%;
    right: -20px;
    transform: translate(-50%, -50%);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    z-index: 2;
    border-radius: var(--border-radius-sm);
    overflow: hidden;
    width: 50px;

    &::before {
      content: "";
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: var(--color-primary);
      filter: blur(10px);
      backdrop-filter: blur(20px);
      opacity: 0.8;
      z-index: 1;
    }
  }

  &__button {
    font-size: 20px;
    padding: 10px;
    color: var(--color-white);
    background-color: transparent;
    user-select: none;
    border: none;
    border-radius: var(--border-radius-sm);
    z-index: 2;
    cursor: pointer;

    &:hover:not(:disabled) {
      opacity: 0.2;
    }

    &:disabled {
      opacity: 0.5;
      cursor: not-allowed;
    }

    &--prev {
      .slider__icon {
        transform: rotate(180deg);
      }
    }

    &--next {
      border-top: 1px solid rgba(255, 255, 255, 0.5);
    }
  }

  &__icon {
    filter: brightness(0) invert(1);
    display: block;
  }
}

@media (max-width: 767px) {
  .slider {
    &__controls {
      position: relative;
      top: auto;
      right: auto;
      transform: none;
      flex-direction: row;
      justify-content: center;
      margin-top: 20px;
      width: 100px;
    }

    &__button--next {
      border-top: none;
      border-left: 1px solid rgba(255, 255, 255, 0.5);
    }

    &__container {
      height: 300px;
      padding: 10px;
    }
  }
}
</style>
