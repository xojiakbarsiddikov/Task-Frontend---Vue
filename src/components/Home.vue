<script setup>
import {computed, onMounted, ref} from "vue";

const search = ref('');
const checkbox = ref(false);
const checkboxes = ref(false);
const checked = ref(null);
const products = [
  {
    id: 1,
    title: `Чистое Небо,<span class="text-span">корпус 10, III кв. 2022 г.</span>`,
    price: "7 733 300 руб.",
    num1: "кв. 62",
    num2: "234.38 м²",
    num3: "1 комн. кв.",
    num4: "7 этаж",
    location: "Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1",
    home: "Квартира",
    label: "Уступка от юр. лица",
    image: "floorpan.png",
    checked: checkbox.value,
    class: "indent",
    active: "red",
    text_left: "text-left1",
    margin: "margin1",
    date: `<span>Добавлено 21/11/2020</span>`,
    model: true,
  },
  {
    id: 2,
    title: `Зеленый квартал на Пулковских высотах, <span class="text-span">корпус 10, III кв. 2022 г.</span>`,
    price: "7 733 300 руб.",
    num1: "кв. 62",
    num2: "234.38 м²",
    num3: "1 комн. кв.",
    num4: "7 этаж",
    location: "Комендантский пр., уч. 1 Каменка",
    label: "Уступка от физ. лица",
    checked: checkbox.value,
    class: "indent",
    active: "blue",
    display: "left",
    text_left: "text-left2",
    margin: "margin2",
    date: `<span>Добавлено 21/11/2020</span>`,
    model: true,
  },
  {
    id: 3,
    title: `Зеленый квартал на Пулковских высотах, <span class="text-span">корпус 10, III кв. 2022 г.</span>`,
    price: "800 300 руб.",
    num1: "№ 7-10-2 (ПИБ №68)",
    num3: "15 м²",
    location: "Ленинградская область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1",
    home: "Паркинг",
    label: "Забронировано",
    image: "car.png",
    active: "greys1",
    checked: checkbox.value,
    text_left: "text-left",
    margin: "margin3",
    date: `<span>Добавлено &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 21/11/2020</span>`,
    model: true,
  },
  {
    id: 4,
    title: `Зеленый квартал на Пулковских высотах, <span class="text-span">корпус 10, III кв. 2022 г.</span>`,
    price: "800 300 руб.",
    num1: "№ 7-10-2 (ПИБ №68)",
    num3: "15 м²",
    location: "Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1",
    home: "Паркинг",
    label: "Продано",
    image: "car.png",
    active: "greys2",
    checked: checkbox.value,
    text_left: "text-left",
    margin: "margin3",
    date: `<span>Добавлено &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 21/11/2020</span>`,
    model: true,
  },
];
const filterAll = () => {
  let checkboxes = document.querySelectorAll('.checkbox')
  checkboxes.forEach((e) => {
    e.checked = true
    products.value.forEach((item) => {
      item.checked = true
    })
  })
};
const deletes = () => {
  products.value.forEach((item) => {
    if(item.checked === true) {
      item.model = false
      products.value = products.value.filter((val) => val !== item)
    }
  })
};
const searchedProducts = computed(() => {
  return products.filter((product) => {
    return (
        product.label
            .indexOf(search.value) !== -1
    );
  });
});
</script>


<template>
  <section>
    <div class="container">
      <div class="filter-wrapper">
        <div class="search">
          <input type="text" v-model="search" placeholder="Введите ЖК / корпус / № квартиры / № паркинга">
          <img src="../assets/image/search.png" alt="search-icon">
        </div>
        <div class="delete df align-center">
          <div class="checkbox-wrapper df align-center">
            <input type="checkbox" v-model="checkboxes" id="checkbox" @change="filterAll">
            <label for="checkbox" class="text-black">все</label>
          </div>
          <div class="delete-wrapper" @click="deletes">
            <button class="df align-center justify-center text-black">
              Удалить
              <img src="../assets/image/delete.png" alt="delete">
            </button>
          </div>
        </div>
      </div>
      <div class="product-wrapper">
        <div class="products-content" v-for="product in searchedProducts" :key="product.id">
          <div class="products">
            <div class="product-content">
              <div class="product-header df align-center justify-flex-end" :class="product.display">
                <h2 class="text-primary">{{ product.price }}</h2>
                <button class="home" v-if="product.image && product.home">
                  <img :src="'/src/assets/image/' + product.image" alt="product-image">
                  <span>{{ product.home }}</span>
                </button>
                <button :class="product.active" class="status">
                  <button class="circle" :class="product.active"></button>
                  {{ product.label }}
                </button>
              </div>
              <div class="product-header-text text-black" :class="product.text_left">
                <p v-html="product.title"></p>
              </div>
              <div class="product-main">
                <div class="wrapper-one df align-center justify-between">
                  <div class="product-one">
                    <div class="wrap df align-center">
                      <div class="checkboxes">
                        <input type="checkbox" v-model="product.checked" class="checkbox">
                      </div>
                      <div class="menu df align-center" :class="product.margin">
                        <ul>
                          <li>{{ product.num1 }}</li>
                          <li>{{ product.num2 }}</li>
                        </ul>
                        <div class="middle-border"></div>
                        <ul>
                          <li>{{ product.num3 }}</li>
                          <li v-if="product.num4">{{ product.num4 }}</li>
                        </ul>
                      </div>
                    </div>
                    <div class="product-footer df align-center">
                      <img src="../assets/image/location.png" alt="location">
                      <p>{{ product.location }}</p>
                    </div>
                  </div>
                  <div class="product-images">
                    <img src="../assets/image/product-image.png" alt="product-image">
                    <p v-html="product.date"></p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="scss">
@import url('https://fonts.googleapis.com/css2?family=PT+Sans:ital,wght@0,700;1,400;1,700&display=swap');
  .filter-wrapper {
    .search {
      position: relative;
      display: flex;
      align-items: center;
      @media(max-width: 600px) {
        margin-top: 50px;
      }
      & input {
        width: 100%;
        outline: none;
        border: 1px solid #C4C4C4;
        padding: 10px 80px;
        font-weight: 400;
        font-size: 14px;
        color: #9B9B9B;
        background: transparent;
      }
      & img {
        position: absolute;
        left: 0;
        transform: translateX(30px);
      }
    }
    .delete {
      padding: 25px 0;
      .checkbox-wrapper {
        & input {
          border: 1px solid #C4C4C4;
          width: 16px;
          height: 16px;
          outline: none;
        }
        & label {
          font-weight: 400;
          font-size: 13px;
          margin: 0 20px 0;
        }
      }
      .delete-wrapper {
        margin: 0 40px 0;
        & button {
          width: 101px;
          height: 38px;
          background: #E5E5E5;
          font-weight: 400;
          font-size: 13px;
          outline: none;
          border: none;
          & img {
            width: 12px;
            height: 14px;
            margin-left: 10px;
          }
        }
      }
    }
  }
.product-wrapper {
  width: 100%;
  overflow: hidden;
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  @media(max-width: 600px) {
    grid-template-columns: 1fr;
    margin-bottom: 50px;
  }
  .product-content {
    height: 250px;
    background: #FFFFFF;
    border: 1px solid #E5E5E5;
    padding: 0 40px;
    @media(max-width: 600px) {
      padding: 0 40px 0 13px;
      height: 280px;
    }
    .product-header {
      margin-top: 20px;
      .home {
        margin: 0 60px 0;
        width: 122.31px;
        height: 26px;
        background: #FFFFFF;
        box-shadow: 0px 0px 2px rgba(94, 119, 157, 0.25);
        border-radius: 32px;
        border: 1px solid #E5E5E5;
        display: flex;
        justify-content: center;
        align-items: center;
        & img {
          margin-right: 10px;
        }
      }
      .status {
        width: 151px;
        height: 30px;
        border: none;
        outline: none;
      }
    }
  }
  .product-header-text {
    & p {
      font-weight: 400;
      font-size: 14px;
      width: 276.65px;
    }
  }
}
.left {
  margin-left: 71px;
  justify-content: space-between!important;
}
.text-left {
  margin: 10px 20px 0 !important;
}
.text-left2 {
  margin: 10px 75px 0!important;
}
.text-left1  {
  margin: 10px 2px 0 !important;
}
.middle-border {
  border: 1px solid #C4C4C4;
  height: 50px;
  width: 2px;
  margin: 0 40px;
}
.menu {
  & ul {
    & li {
      font-weight: 400;
      font-size: 14px;
      line-height: 25px;
      color: #000000;
    }
  }
}
.margin1 {
  margin-left: 25px;
}
.margin2 {
  margin-left: 65px;
}
.margin3 {
  margin-left: 39px;
}
.circle {
  width: 6px;
  height: 6px;
  border-radius: 50px;
  border: none;
}
.product-images {
  & p {
    font-weight: 400;
    font-size: 13px;
    color: #9B9B9B;
    margin: 10px 0;
    text-align: right;
  }
}
.product-footer {
  margin: 15px 30px 0;
  & p {
    font-weight: 400;
    font-size: 14px;
    color: #000000;
    width: 225px;
    line-height: 20px;
    margin: 0 10px 0;
  }
}
.product-one {
  margin: 10px 0 0;
}
.checkbox {
  border: 1px solid #C4C4C4;
  &:checked {
    background: #FCE66F;
  }
}
</style>