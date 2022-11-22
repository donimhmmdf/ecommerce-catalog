<template>
  <div
    v-if="!loading"
    :class="
      products.category == 'men\'s clothing'
        ? 'container-men'
        : 'container-women' && products.category == 'women\'s clothing'
        ? 'container-women'
        : 'container-men' && products.category == 'electronics'
        ? 'container-unvailable'
        : 'container-unvailable'
    "
  >
    <section
      v-if="
        products.category == 'men\'s clothing' ||
        products.category == 'women\'s clothing'
      "
    >
      <div class="card">
        <div class="flex-wrap">
          <div class="left">
            <img :src="products.image" alt="" />
          </div>
          <div class="right">
            <h2
              :class="
                products.category == 'men\'s clothing'
                  ? 'title-men'
                  : 'title-women'
              "
            >
              {{ products.title }}
            </h2>
            <div class="rating-category">
              <p class="category">{{ products.category }}</p>
              <div class="rating">
                <p>{{ products.rating.rate }}/5.0</p>
                <span
                  :class="
                    products.category == 'men\'s clothing'
                      ? 'dot-men'
                      : 'dot-women'
                  "
                ></span>
                <span
                  :class="
                    products.category == 'men\'s clothing'
                      ? 'dot-men'
                      : 'dot-women'
                  "
                ></span>
                <span
                  :class="
                    products.category == 'men\'s clothing'
                      ? 'dot-men'
                      : 'dot-women'
                  "
                ></span>
                <span
                  :class="
                    products.category == 'men\'s clothing'
                      ? 'dot-men-empty'
                      : 'dot-women-empty'
                  "
                ></span>
                <span
                  :class="
                    products.category == 'men\'s clothing'
                      ? 'dot-men-empty'
                      : 'dot-women-empty'
                  "
                ></span>
              </div>
            </div>
            <hr style="width: 100%; text-align: left; margin-left: 0" />
            <p class="description">{{ products.description.slice(0, 150) }}</p>
            <hr style="width: 100%; text-align: left; margin-left: 0" />
            <h3
              :class="
                products.category == 'men\'s clothing'
                  ? 'price-men'
                  : 'price-women'
              "
            >
              ${{ products.price }}
            </h3>
            <div class="button">
              <button
                :class="
                  products.category == 'men\'s clothing'
                    ? 'buy-btn-men'
                    : 'buy-btn-women'
                "
              >
                Buy now
              </button>
              <button
                :class="
                  products.category == 'men\'s clothing'
                    ? 'next-btn-men'
                    : 'next-btn-women'
                "
                @click.prevent="btnNext()"
              >
                Next product
              </button>
            </div>
          </div>
        </div>
      </div>
    </section>
    <section v-else>
      <div class="card">
        <img class="unvailable-img" src="@/assets/unvailable.png" alt="" />
        <div class="description-unvailable">
          <h2>This product is unvailable to show</h2>
          <button class="unvailable-btn" @click.prevent="btnNext()">
            Next product
          </button>
        </div>
      </div>
    </section>
  </div>
  <div class="loading" v-else>
    <div class="loader"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      index: 1,
      loading: true,
      loadingImage: require("../assets/hourglass.gif"),
    };
  },
  methods: {
    async fetchData() {
      const response = await fetch(
        "https://fakestoreapi.com/products/" + this.index
      );
      const data = await response.json();
      this.loading = false;
      this.products = data;
    },
    btnNext() {
      if (this.index < 20) {
        this.index++;
        this.fetchData();
      } else {
        this.index = 1;
      }
      console.log(this.index);
    },
  },
  created() {
    this.loading = true;
    this.fetchData();
  },
};
</script>

<style></style>
