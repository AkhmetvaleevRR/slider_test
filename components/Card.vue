<template>
  <article class="card" @click="handleClick">
    <div class="card__info">
      <div class="card__info-skew">
        <div class="card__info-content">
          <time class="card__date">до {{ date }}</time>
          <p class="card__description">{{ description }}</p>
          <button class="card__action-btn">
            <img
              src="~/assets/icons/Arrow.svg"
              alt="стрелка"
              class="card__arrow-icon"
            />
          </button>
        </div>
      </div>
    </div>

    <div class="card__image">
      <div class="card__image-skew">
        <img :src="image" :alt="description" class="card__image-content" />
      </div>
      <div class="card__image-tag">
        <img
          src="~/assets/icons/geotag.svg"
          alt="метка"
          class="card__tag-icon"
        />
        {{ tag }}
      </div>
    </div>
  </article>
</template>

<script setup>
const router = useRouter();

const props = defineProps({
  image: String,
  description: String,
  tag: String,
  date: String,
});

const handleClick = () => {
  router.push({
    path: "/about",
    query: {
      image: props.image,
      description: props.description,
      tag: props.tag,
      date: props.date,
    },
  });
};
</script>

<style lang="scss" scoped>
.card {
  display: flex;
  width: 400px;
  height: 200px;
  padding: 10px;
  cursor: pointer;

  // Адаптив
  @media (max-width: 1200px) {
    height: 300px;
    flex-direction: column;
  }
}

// image
.card__image {
  height: 100%;
  overflow: hidden;
  border-radius: 0 20px 20px 0;
  position: relative;
  padding-left: 24px;
  transition: transform 0.3s ease;

  // Адаптив
  @media (max-width: 1200px) {
    border-radius: 20px;
    padding-left: 0;
    padding-top: 44px;
    margin-top: 10px;
  }

  &:hover {
    transform: scale(1.1);
  }
}

.card__image-skew {
  display: flex;
  align-items: center;
  border-radius: 16px;
  transform: skew(-13deg, 0);
  background: #c8c2c2;
  height: inherit;
  width: 100%;
  overflow: hidden;
  padding-right: 20px;
  transition: transform 0.3s ease;

  // Адаптив
  @media (max-width: 1200px) {
    width: 100%;
    transform: skew(0, -5deg);
    padding-bottom: 20px;
    padding-right: 0;
    overflow: hidden;
  }
}

.card__image-content {
  height: 100%;
  width: auto;
  border-radius: 16px;
  transition: transform 0.3s ease;
  transform: skew(13deg, 0);
  overflow: hidden;
  margin-left: -20px;

  @media (max-width: 1200px) {
    transform: skew(0, 5deg);
    overflow: hidden;
    width: 100%;
    height: auto;
    margin-left: 0;
    margin-bottom: -48px;
  }
}

.card__image-tag {
  position: absolute;
  bottom: 10px;
  right: 10px;
  display: flex;
  align-items: center;
  text-transform: uppercase;
  gap: 5px;
  color: var(--color-primary);
  background-color: var(--color-white);
  font-size: 10px;
  font-weight: 500;
  padding: 5px 8px;
  border-radius: var(--border-radius-md);

  // Планшет
  @media (max-width: 1024px) {
    font-size: 9px;
    padding: 4px 6px;
  }
}

// info
.card__info {
  width: 100%;
  overflow: hidden;
  border-radius: 16px;
  font-size: 16px;
  position: relative;
  margin-top: 15px;
  margin-right: -30px;
  margin-left: 10px;

  // Адаптив
  @media (max-width: 1200px) {
    height: 200px;
    border-radius: 16px;
    margin-left: 0;
    padding-bottom: 54px;
    margin-bottom: -60px;
  }
}

.card__info-skew {
  display: inline-block;
  border-radius: 16px;
  overflow: hidden;
  transform: skew(-13deg, 0);
  margin-left: -20px;
  height: 100%;
  width: 100%;
  box-sizing: border-box;

  // Адаптив
  @media (max-width: 1200px) {
    transform: skew(0, -5deg);
    margin-left: 0;
    height: 160px;
    margin-top: -30px;
  }
}

.card__info-content {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 100%;
  width: 100%;
  transform: skew(13deg, 0);
  background-color: var(--color-background);
  margin-left: 20px;
  padding: 15px;
  box-sizing: border-box;
  position: relative;

  // Адаптив
  @media (max-width: 1200px) {
    height: max-content;
    transform: skew(0, 5deg);
    margin-left: 0;
    padding-top: 50px;
  }

  &::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: linear-gradient(
      to bottom right,
      var(--color-soft-blue),
      var(--color-accent-blue)
    );
    opacity: 0;
    transition: opacity 0.3s ease;
  }

  &:hover {
    color: var(--color-white);

    &::before {
      opacity: 1;
    }
  }

  & > * {
    position: relative;
    z-index: 1;
  }

  & p {
    margin-top: 0;
  }
}

.card__description {
  position: relative;
  z-index: 2;
}

.card__date {
  width: max-content;
  background: linear-gradient(
    to bottom right,
    var(--color-soft-blue),
    var(--color-accent-blue)
  );
  color: var(--color-white);
  border-radius: var(--border-radius-sm);
  padding: 9px 12px;
  font-size: 10px;
  margin: 0;
  transition: background-color 0.3s ease, color 0.3s ease;
  position: relative;
  z-index: 2;

  // Планшет
  @media (max-width: 1024px) {
    padding: 7px 10px;
    font-size: 9px;
  }
}

.card__info-content:hover {
  & .card__date {
    background: var(--color-white);
    color: var(--color-primary);
  }
}

// button
.card__action-btn {
  height: 40px;
  width: 40px;
  border-radius: var(--border-radius-sm);
  border: 0;
  background-color: var(--color-white);
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;

  // Планшет
  @media (max-width: 1024px) {
    height: 35px;
    width: 35px;
    margin-bottom: 60px;
  }

  // Адаптив
  @media (max-width: 1200px) {
    align-self: flex-start;
  }

  &:hover {
    background-color: var(--color-dark-blue);

    .card__arrow-icon {
      filter: brightness(0) invert(1);
    }
  }
}
</style>
