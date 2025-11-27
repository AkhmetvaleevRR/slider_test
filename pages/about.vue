<template>
  <main class="dashboard">
    <header class="dashboard__header">
      <button
        class="dashboard__back-btn"
        @click="handleBack"
        aria-label="Вернуться назад"
      >
        <svg
          class="dashboard__back-icon"
          width="24"
          height="24"
          viewBox="0 0 24 24"
          fill="none"
        >
          <path
            d="M15 18L9 12L15 6"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
        Назад
      </button>
      <h1 class="dashboard__title">Проект это</h1>
    </header>

    <div class="dashboard__body">
      <section class="dashboard__stats" aria-labelledby="stats-title">
        <h2 id="stats-title" class="dashboard__stats-title">стабильность</h2>
        <div class="dashboard__stats-list">
          <article class="dashboard__stat-item">
            <div class="dashboard__stat-number">15+</div>
            <p class="dashboard__stat-description">
              лет успешной работы на рынке Краснодара
            </p>
          </article>
          <article class="dashboard__stat-item">
            <div class="dashboard__stat-number">
              1 <small class="dashboard__stat-unit">млн м²</small>
            </div>
            <p class="dashboard__stat-description">квадратных метров сданного жилья</p>
          </article>
          <article class="dashboard__stat-item">
            <div class="dashboard__stat-number">6 000+</div>
            <p class="dashboard__stat-description">довольных семей</p>
          </article>
        </div>
        <footer class="dashboard__stats-footer">— Результат надежной работы</footer>
      </section>

      <section class="dashboard__features">
        <article class="dashboard__feature dashboard__feature--development">
          <div class="dashboard__feature-skew">
            <div class="dashboard__feature-content">
              <h3 class="dashboard__feature-title">развитие</h3>
              <p class="dashboard__feature-text">
                Мы постоянно совершенствуем проекты и внедряем новые решения.
                Создаем современные жилые районы с развитой инфраструктурой для
                комфортной жизни
              </p>
            </div>
          </div>
        </article>

        <article class="dashboard__feature dashboard__feature--team">
          <div class="dashboard__feature-skew">
            <h3 class="dashboard__feature-title">команда</h3>
            <div class="dashboard__feature-content">
              <div class="dashboard__feature-text-content">
                <p class="dashboard__feature-text">
                  Нас объединяет ответственность за качество, профессионализм
                  и забота о клиентах. Вместе мы создаем дома, где хочется жить.
                </p>
              </div>
              <figure class="dashboard__feature-image">
                <img
                  src="https://placebear.com/300/300"
                  alt="Член команды проекта"
                  class="dashboard__feature-photo"
                  loading="lazy"
                />
              </figure>
            </div>
          </div>
        </article>
      </section>
    </div>
  </main>
</template>

<script setup>
const router = useRouter();

const handleBack = () => {
  router.back();
};
</script>

<style lang="scss">
.dashboard {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;

  &__header {
    margin-bottom: 30px;
    position: relative;
  }

  &__back-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 8px 16px;
    background: transparent;
    border: 1px solid var(--color-primary);
    border-radius: var(--border-radius-sm);
    color: var(--color-primary);
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
    margin-bottom: 15px;

    &:hover {
      background: var(--color-primary);
      color: var(--color-white);
    }

    &:focus {
      outline: 2px solid var(--color-accent-blue);
      outline-offset: 2px;
    }
  }

  &__back-icon {
    transition: transform 0.3s ease;
  }

  &__back-btn:hover &__back-icon {
    transform: translateX(-2px);
  }

  &__title {
    font-size: 38px;
    font-weight: 600;
    text-transform: uppercase;
    margin: 0;
  }

  &__body {
    display: flex;
    gap: 30px;
  }

  // Stats section
  &__stats {
    flex: 1;
    background: var(--color-background);
    border-radius: var(--border-radius-lg);
    padding: 30px;
    position: relative;
    min-height: 400px;
  }

  &__stats-title {
    font-size: 24px;
    font-weight: 600;
    margin: 0 0 50px;
    text-transform: uppercase;
  }

  &__stats-list {
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  &__stat-item {
    display: flex;
    gap: 33px;
    align-items: center;
  }

  &__stat-number {
    font-size: 46px;
    font-weight: 700;
    background: linear-gradient(
      to bottom right,
      var(--color-blue),
      var(--color-light-blue)
    );
    -webkit-background-clip: text;
    background-clip: text;
    -webkit-text-fill-color: transparent;

    small {
      font-size: 20px;
      font-weight: 500;
    }
  }

  &__stat-unit {
    font-size: 20px;
    font-weight: 500;
  }

  &__stat-description {
    font-size: 16px;
    color: var(--color-secondary);
    font-weight: 500;
    margin: 0;
    width: 50%;
  }

  &__stats-footer {
    padding: 40px;
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    border-radius: var(--border-radius-lg);
    font-size: 26px;
    font-weight: 600;
    background: linear-gradient(
      to bottom right,
      #cdd9e9,
      rgba(205, 217, 233, 0.2)
    );
  }

  // Features section
  &__features {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 24px;
  }

  &__feature {
    border-radius: 16px;

    &--development {
      border-radius: 16px 16px 0 0;
      overflow: hidden;

      .dashboard__feature-content {
        transform: skewY(5deg);
        margin-top: 60px;
        margin-left: 20px;
      }

      .dashboard__feature-skew {
        height: 200px;
        overflow: hidden;
        transform: skewY(-5deg);
        border-radius: 16px;
        background-color: var(--color-light-blue);
        margin-top: -45px;
        margin-bottom: 45px;
      }

      .dashboard__feature-title {
        margin-bottom: 10px;
        font-size: 26px;
      }

      .dashboard__feature-text {
        font-size: 18px;
        font-weight: 400;
        letter-spacing: 0;
      }

      .dashboard__feature-text,
      .dashboard__feature-title {
        color: var(--color-white);
      }
    }

    &--team {
      transform: translateY(-50px);
      overflow: hidden;
      margin-top: -24px;
      padding-top: 24px;
      border-bottom: 1px solid var(--color-primary);

      .dashboard__feature-skew {
        height: 200px;
        transform: skewY(-5deg);
        border-radius: 16px;
        border: 1px solid var(--color-primary);
        margin-bottom: -25px;
        overflow: hidden;
      }

      .dashboard__feature-content {
        transform: skewY(5deg);
        display: flex;
        gap: 15px;
        margin-top: -45px;
        padding-top: 45px;
        padding-left: 15px;
      }

      .dashboard__feature-title {
        padding-top: 25px;
        padding-left: 15px;
        transform: skewY(5deg);
      }
    }
  }

  &__feature-title {
    font-size: 18px;
    font-weight: 600;
    margin: 0;
    text-transform: uppercase;
  }

  &__feature-text {
    margin: 4px 0;
    color: var(--color-secondary);
    font-size: 16px;
    font-weight: 500;
  }

  &__feature-text-content {
    flex: 1;
  }

  &__feature-image {
    width: 40%;
    margin: 0;
    margin-top: -70px;
  }

  &__feature-photo {
    border-radius: 8px;
    width: 100%;
    height: auto;
  }
}

// Адаптив
@media (max-width: 1200px) {
  .dashboard {
    &__stats-footer {
      font-size: 20px;
    }
  }
}

@media (max-width: 1024px) {
  .dashboard {
    &__body {
      flex-direction: column;
      gap: 20px;
    }

    &__feature--team {
      margin-top: -30px;
      padding-top: 40px;

      .dashboard__feature-skew {
        margin-top: 5px;
        margin-bottom: -45px;
      }

      .dashboard__feature-title {
        padding-top: 60px;
      }

      .dashboard__feature-image {
        margin-top: -130px;
      }
    }
  }
}

@media (max-width: 768px) {
  .dashboard {
    &__title {
      font-size: 32px;
    }

    &__stats {
      padding: 20px;
    }

    &__stat-item {
      flex-direction: column;
      gap: 15px;
      text-align: center;
    }

    &__stat-description {
      width: 100%;
    }

    &__stats-footer {
      padding: 20px;
      font-size: 18px;
    }

    &__feature--team {
      .dashboard__feature-title {
        padding-top: 40px;
      }

      .dashboard__feature-content {
        flex-direction: column;
      }

      .dashboard__feature-image {
        margin-top: 0;
        text-align: center;
      }
    }
  }
}

@media (max-width: 480px) {
  .dashboard {
    padding: 15px;

    &__title {
      font-size: 28px;
    }

    &__stat-number {
      font-size: 36px;
    }

    &__stat-unit {
      font-size: 16px;
    }
  }
}
</style>