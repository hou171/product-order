<script>
import ProductSwiper from '@/components/ProductSwiper.vue'

import mug from '@/images/馬克杯.jpg';
import wirelessMouse from '@/images/無線滑鼠.png';
import bluetoothHeadphones from '@/images/藍牙耳機.jpg';
import backpack from '@/images/雙肩背包.jpg';
import thermos from '@/images/環保保溫杯.jpg';
import powerBank from '@/images/便攜式充電寶.jpg';
import deskLaptopStand from '@/images/筆記型電腦支架.jpg';
import eReader from '@/images/電子閱讀器.png';
import foldingParasol from '@/images/折疊式遮陽傘.jpg';
import leatherWatch from '@/images/簡約皮革手錶.jpg';

export default {
  components: {
    ProductSwiper,
  },
  data() {
    return {
      products: [
        { id: 1, name: '經典咖啡杯', price: 150, description: '優雅設計，適合各種場合使用', photo: mug },
        { id: 2, name: '無線滑鼠', price: 500, description: '人體工學設計，舒適操作', photo: wirelessMouse },
        { id: 3, name: '藍牙耳機', price: 1200, description: '高音質，長效電池續航', photo: bluetoothHeadphones },
        { id: 4, name: '雙肩背包', price: 850, description: '輕便耐用，多功能收納', photo: backpack },
        { id: 5, name: '環保保溫杯', price: 300, description: '長效保溫，環保材質', photo: thermos },
        { id: 6, name: '便攜式充電寶', price: 600, description: '大容量，快速充電，輕巧便攜', photo: powerBank },
        { id: 7, name: '筆記型電腦支架', price: 700, description: '可調節高度，改善姿勢，散熱效果好', photo: deskLaptopStand },
        { id: 8, name: '電子閱讀器', price: 3500, description: '高解析度螢幕，長效電池，大容量存儲', photo: eReader },
        { id: 9, name: '折疊式遮陽傘', price: 250, description: '輕量化設計，防UV，便於攜帶', photo: foldingParasol },
        { id: 10, name: '簡約皮革手錶', price: 1800, description: '精緻工藝，百搭款式，防水設計', photo: leatherWatch },
      ],
    };
  },
  methods: {
    goToOrder(product) {
      localStorage.setItem('product', JSON.stringify(product));
      this.$router.push({
        name: 'order',
        params: {
          id: product.id.toString(),
        },
        query: {
          name: product.name,
        },
      })
    },
    scrollToTop() {
      window.scrollTo({
        top: 0,
        behavior: 'smooth',
      });
    }
  },
}
</script>

<template>
  <div id="app">
    <div class="container">
      <ProductSwiper :products="products" />
      <h1>產品展示</h1>
      <div class="content">
        <div class="product" v-for="product in products" :key="product.id" data-aos="zoom-in">
          <h2>{{ product.name }}</h2>
          <img :src=product.photo :alt=product.photo>
          <p class="price">NT${{ product.price }}</p>
          <p class="description">{{ product.description }}</p>
          <button type="button" class="btn" @click="goToOrder(product)">購買</button>
        </div>
      </div>
    </div>
    <button class="go-top" @click="scrollToTop">TOP</button>
  </div>
</template>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  justify-content: center;
  padding: 20px;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.content {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

h1 {
  color: #333;
  text-align: center;
}

.product {
  border: 1px solid #ddd;
  padding: 20px;
  margin-bottom: 20px;
  border-radius: 5px;
}

.product img {
  aspect-ratio: 1/1;
  width: 100%;
  object-fit: cover;
  margin-bottom: 15px;
}

.product h2 {
  color: #444;
}

.price {
  font-weight: bold;
  color: #28a745;
}

.description {
  margin-bottom: 15px;
}

.btn {
  display: inline-block;
  background-color: #007bff;
  color: #fff;
  padding: 10px 15px;
  text-decoration: none;
  border-radius: 3px;
  border: 0;
  cursor: pointer;
  transition: background-color 0.3s;
}

.btn:hover {
  background-color: #0056b3;
}

.go-top {
  position: fixed;
  bottom: 20px;
  right: 20px;
  background-color: #007bff;
  color: white;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;
  z-index: 9;
}

.go-top:hover {
  background-color: #0056b3;
  transform: translateY(-2px);
}
</style>