<template>
  <section class="exclusive-features">
    <div class="exclusive-features__header">
      <div class="row">
        <div class="col-xl-7 col-xl-offset-1 col-lg-4 col-lg-offset-0 col-md-6">
          <h2 class="exclusive-features__title title-lg tt-uppercase">
            {{ title }}
          </h2>
        </div>
      </div>
    </div>
    <div class="exclusive-features__body">
      <div class="row">
        <div class="col-xl-5 col-xl-offset-1 col-lg-offset-0 col-md-6">
          <div class="exclusive-features__main-content">
            <div class="exclusive-features__preview">
              <img
                :src="preview"
                class="exclusive-features__image-preview"
                v-show="preview"
              />
              <img
                src="@/assets/img/news/void-logo.svg"
                class="exclusive-features__placeholder-preview"
                v-show="!preview"
              />
            </div>
            <div
              class="exclusive-features__main-list"
              v-show="featureListMain && featureListMain.length"
            >
              <ExclusiveFeaturesList
                class="exclusive-features__features-list"
                :exclusiveFeaturesList="featureListMain"
              />
            </div>
          </div>
        </div>
        <div
          class="col-xl-4 col-xl-offset-1 col-md-6 col-md-offset-0"
          v-show="featureListSecondary && featureListSecondary.length"
        >
          <div class="exclusive-features__info-content">
            <ExclusiveFeaturesList
              class="exclusive-features__secondary-list"
              :exclusiveFeaturesList="featureListSecondary"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="exclusive-features__footer" v-show="serviceSlug">
      <div class="row">
        <div
          class="col-xl-10 col-xl-offset-2 col-lg-offset-1 col-md-6 col-md-offset-0"
        >
          <h3 class="exclusive-features__title-footer tt-uppercase title-md">
            Продажа оборудования
          </h3>
          <nuxt-link
            :to="{ name: 'services-slug', params: { slug: serviceSlug } }"
          >
            <CustomButton
              class="exclusive-features__link-to-service"
              :theme="ButtonTheme.ACCENT_OUTER"
              :size="ButtonSize.MD"
              :disabledClick="true"
            >
              Перейти к услуге
            </CustomButton>
          </nuxt-link>
        </div>
      </div>
    </div>
  </section>
</template>

<script lang="ts">
import { Vue, Component, Prop } from "nuxt-property-decorator";
import { ITechnology } from "~/types/pages/PartnersPageData";
import ExclusiveFeaturesList from "@/components/pages/partners/ExclusiveFeatures/ExclusiveFeaturesList.vue";
import { ButtonSize, ButtonTheme } from "~/types/common";
import CustomButton from "@/components/common/controls/CustomButton.vue";
@Component({ components: { ExclusiveFeaturesList, CustomButton } })
export default class ExclusiveFeatures extends Vue {
  @Prop() title: string;
  @Prop() preview: string;
  @Prop() featureList: Array<ITechnology>;
  @Prop() serviceSlug: string;

  ButtonTheme: typeof ButtonTheme = ButtonTheme;
  ButtonSize: typeof ButtonSize = ButtonSize;

  get countItemsInFeatureListMain() {
    // распределение текстовых блоков в левую часть под превью и в правую часть
    // в правой части всегда больше на 1айтем или такое же кол-во, как и слева при четном кол-ве общих айтемов
    return !this.featureList.length
      ? 0
      : Math.floor(this.featureList.length / 2);
  }

  get featureListMain() {
    return this.featureList.filter(
      (item, index) => index < this.countItemsInFeatureListMain
    );
  }

  get featureListSecondary() {
    return this.featureList.filter(
      (item, index) => index >= this.countItemsInFeatureListMain
    );
  }
}
</script>

<style lang="less">
.exclusive-features {
  // .exclusive-features__header
  &__header {
    margin-bottom: 109px;

    @media (max-width: @breakpoint-desktop-lg) {
      margin-bottom: 80px;
    }
    @media screen and (max-width: @breakpoint-tablet) {
      margin-bottom: 43px;
    }

    @media screen and (max-width: @breakpoint-tablet-sm) {
      margin-bottom: 35px;
    }
  }

  // .exclusive-features__preview
  &__preview {
    width: 100%;
    height: 406px;
    background-color: @color-secondary-light;
    margin-bottom: 79px;

    display: flex;
    align-items: center;
    justify-content: center;

    @media (max-width: @breakpoint-desktop-lg) {
      margin-bottom: 80px;
    }
    @media screen and (max-width: @breakpoint-tablet) {
      height: 375px;
      margin-bottom: 43px;
    }

    @media screen and (max-width: @breakpoint-tablet-md) {
      height: 257px;
    }

    @media screen and (max-width: @breakpoint-tablet-sm) {
      height: 448px;
      margin-bottom: 32px;
    }

    @media screen and (max-width: @breakpoint-mob) {
      height: 250px;
    }
  }
  // .exclusive-features__image-preview
  &__image-preview {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }

  // .exclusive-features__placeholder-preview
  &__placeholder-preview {
    width: 75px;
    height: 75px;
  }

  // .exclusive-features__main-list
  &__main-list {
    display: grid;
    gap: 0 30px;
    grid-template-columns: repeat(5, 1fr);
    @media screen and (max-width: @breakpoint-tablet-sm) {
      display: block;
    }
  }

  // .exclusive-features__features-list
  &__features-list {
    grid-column: ~"2/6";
  }

  // .exclusive-features__info-content
  &__info-content {
    @media screen and (max-width: @breakpoint-tablet-sm) {
      margin-top: 35px;
    }
  }

  // .exclusive-features__footer
  &__footer {
    margin-top: 146px;
    @media (max-width: @breakpoint-desktop-lg) {
      margin-top: 100px;
    }

    @media screen and (max-width: @breakpoint-tablet) {
      margin-top: 85px;
    }

    @media screen and (max-width: @breakpoint-tablet-sm) {
      margin-top: 51px;
    }
  }

  // .exclusive-features__title-footer
  &__title-footer {
    margin-bottom: 45px;

    @media screen and (max-width: @breakpoint-tablet) {
      margin-bottom: 38px;
    }

    @media screen and (max-width: @breakpoint-tablet-sm) {
      margin-bottom: 22px;
    }
  }
}
</style>
