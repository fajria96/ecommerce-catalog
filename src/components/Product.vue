<template>
  <div :class="productClass">
    <div class="product-wrapper">
      <div class="product-card">
        <div class="product-image">
          <img :src="product.image" :alt="product.title" />
        </div>
        <div class="product-details">
          <h2 class="product-title">{{ product.title }}</h2>
          <p
            class="product-category"
            :class="{
              category: product.category === 'men\'s clothing',
              category: product.category === 'women\'s clothing',
            }"
          >
            {{ product.category }}
          </p>
          <p class="product-description">{{ product.description }}</p>
          <p class="product-price">${{ product.price }}</p>
          <button
            class="buy-now"
            :class="{
              'btn-buy-men': product.category === 'men\'s clothing',
              'btn-buy-women': product.category === 'women\'s clothing',
            }"
          >
            Buy now
          </button>
          <button
            class="next-product"
            :class="{
              'btn-men': product.category === 'men\'s clothing',
              'btn-women': product.category === 'women\'s clothing',
            }"
            @click="fetchNextProduct()"
          >
            Next Product
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      index: 1,
      product: {},
      productClass: "",
    };
  },
  methods: {
    fetchProduct() {
      fetch(`https://fakestoreapi.com/products/${this.index}`)
        .then((response) => response.json())
        .then((data) => {
          if (
            data.category === "men's clothing" ||
            data.category === "women's clothing"
          ) {
            this.product = data;
            this.setProductClass(data.category);
          } else {
            this.fetchNextProduct();
          }
        })
        .catch((error) => {
          console.log(error);
        });
    },
    fetchNextProduct() {
      this.index = this.index === 20 ? 1 : this.index + 1;
      this.fetchProduct();
    },
    setProductClass(category) {
      if (category === "men's clothing") {
        this.productClass = "page-men";
      } else if (category === "women's clothing") {
        this.productClass = "page-women";
      } else {
        this.productClass = "page-unavailable";
      }
    },
  },
  mounted() {
    this.fetchProduct();
  },
};
</script>

<style>
:root {
  --background-men: #d6e6ff;
  --background-women: #fde2ff;
  --primary-color: #f5b92e;
  --women-color: #720060;
  --men-color: #002772;
  --unavailable-color: #d8d7d7;
}

.product-wrapper {
  width: 100%;
  height: 420px;
  display: flex;
  justify-content: center;
}

.product-card {
  position: absolute;
  display: flex;
  flex-direction: row;
  align-items: center;
  padding: 16px;
  width: 1034px;
  height: 480px;
  left: 100px;
  top: 123px;
  background: #ffffff;
  box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.25);
  border-radius: 10px;
}

.page-men {
  background-color: var(--background-men);
  color: var(--men-color);
}

.page-women {
  background-color: var(--background-women);
  color: var(--women-color);
}

.page-unavailable {
  background-color: var(--unavailable-color);
  color: var(--unavailable-color);
}

.product-image {
  flex-basis: 40%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.product-image img {
  max-width: 50%;
}

.product-details {
  flex-basis: 50%;
  padding-left: 16px;
}

.product-title {
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 34px;
}

.product-price {
  font-size: 20px;
  margin: 16px 0;
}

.product-category {
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #3f3f3f;
}

.product-description {
  top: 20px;
  bottom: 20px;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 24px;
  color: #1e1e1e;
  border-top: 1px solid lightgrey;
  border-bottom: 1px solid lightgrey;
}

.next-product {
  padding: 8px 60px;
  border-radius: 4px;
  margin-top: 16px;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 24px;
}

button:hover {
  cursor: pointer;
}

.btn-men {
  background-color: white;
  color: var(--men-color);
  border: 3px solid var(--men-color);
}

.btn-women {
  background-color: white;
  color: var(--women-color);
  border: 1px solid var(--women-color);
}

.buy-now {
  padding: 8px 80px;
  border-radius: 4px;
  margin-top: 16px;
  font-style: normal;
  font-weight: 500;
  font-size: 20px;
  line-height: 24px;
  margin-right: 30px;
}

.btn-buy-men {
  background-color: var(--men-color);
  color: white;
}

.btn-buy-women {
  background-color: var(--women-color);
  color: white;
}
/* phone */
@media only screen and (min-width: 480px) {
  .product-wrapper {
    display: flex;
    align-items: center;
  }
  .product-card {
    flex-direction: column;
    height: 800px;
    max-width: 250px;
    margin: auto;
    text-align: center;
  }

  .product-title {
    font-size: 1rem;
    margin-top: 0.5rem;
    margin-bottom: 0.25rem;
  }

  .product-category {
    font-size: 0.8rem;
  }

  .product-image {
    height: 350px;
    width: 350px;
  }

  .buy-now {
    padding: 4px 20px;
    font-size: 10px;
  }

  .next-product {
    padding: 4px 20px;
    font-size: 10px;
  }
}

@media only screen and (min-width: 560px) {
  .product-wrapper {
    display: flex;
    align-items: center;
  }
  .product-card {
    flex-direction: column;
    height: 680px;
    max-width: 490px;
    margin: auto;
    text-align: left;
  }

  .product-title {
    font-size: 1rem;
    margin-top: 0.5rem;
    margin-bottom: 0.25rem;
  }

  .product-category {
    font-size: 0.8rem;
  }

  .product-image {
    height: 350px;
    width: 350px;
  }

  .buy-now {
    padding: 8px 80px;
    font-weight: 400;
    font-size: 16px;
  }

  .next-product {
    padding: 8px 60px;
    font-weight: 400;
    font-size: 16px;
  }
}

/* tablet */
@media only screen and (min-width: 768px) {
  .product-wrapper {
    display: flex;
  }
  .product-card {
    flex-direction: row;
    height: 480px;
    max-width: 710px;
    margin: auto;
    text-align: left;
  }

  .product-title {
    font-size: 1rem;
    margin-top: 0.5rem;
    margin-bottom: 0.25rem;
  }

  .product-category {
    font-size: 0.8rem;
  }

  .buy-now {
    padding: 8px 50px;
    font-weight: 400;
    font-size: 16px;
  }

  .next-product {
    padding: 8px 30px;
    font-weight: 400;
    font-size: 16px;
  }
}

/* desktop */
@media only screen and (min-width: 992px) {
  .product-card {
    flex-direction: row;
    height: 480px;
    max-width: 1034px;
    margin: auto;
    text-align: left;
  }

  .product-title {
    font-size: 1rem;
    margin-top: 0.5rem;
    margin-bottom: 0.25rem;
  }

  .product-category {
    font-size: 0.8rem;
  }

  .buy-now {
    padding: 8px 80px;
    font-weight: 500;
    font-size: 20px;
  }

  .next-product {
    padding: 8px 60px;
    font-weight: 500;
    font-size: 20px;
  }
}
</style>
