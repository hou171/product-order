<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Autoplay, Pagination, Navigation } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/pagination';
import 'swiper/css/navigation';

export default {
    name: 'ProductSwiper',
    components: {
        Swiper,
        SwiperSlide,
    },
    props: {
        products: {
            type: Array,
            required: true,
        }
    },
    data() {
        return {
            swiperModules: [Autoplay, Pagination, Navigation],
            swiperOptions: {
                slidesPerView: 1, // 同時顯示的投影片數量 1
                spaceBetween: 30, // 投影片之間的間距 30px
                loop: true, // 循環播放
                autoplay: {
                    delay: 6000, // 每張投影片停留秒數 6秒
                },
                pagination: {
                    clickable: true, // 分頁點擊
                },
                navigation: true, // 前後箭頭
            }
        };
    },
}
</script>

<template>
    <div class="container">
        <swiper :modules="swiperModules" v-bind="swiperOptions" class="mySwiper">
            <swiper-slide v-for="product in products" :key="product.id">
                <div class="content">
                    <img :src="product.photo" :alt="product.name">
                </div>
            </swiper-slide>
        </swiper>
    </div>
</template>

<style scoped>
.container {
    margin-bottom: 40px;
    border-radius: 10px;
    overflow: hidden;
}

.mySwiper {
    width: 100%;
    height: 400px;
}

.content {
    position: relative;
    width: 100%;
    height: 100%;
}

.content img {
    width: 100%;
    height: 100%;
    object-fit: contain;
}

.info {
    position: absolute;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 20px;
    background: rgba(0, 0, 0, 0.5);
    color: white;
    transition: transform 0.3s ease;
}

.info h3 {
    margin: 0;
    font-size: 24px;
}

.price {
    margin: 10px 0 0;
    font-size: 20px;
    color: #4CAF50;
}

.description {
    font-size: 14px;
    margin: 5px 0 0;
    opacity: 0.8;
}

:deep(.swiper-button-prev),
:deep(.swiper-button-next) {
    color: white;
    background: rgba(0, 0, 0, 0.5);
    width: 40px;
    height: 40px;
    border-radius: 50%;
}

:deep(.swiper-button-prev:after),
:deep(.swiper-button-next:after) {
    font-size: 20px;
}

:deep(.swiper-pagination-bullet) {
    background: white;
    border: 1px solid gray;
    opacity: 0.7;
}

:deep(.swiper-pagination-bullet-active) {
    background: #4CAF50;
}

@media (max-width: 768px) {
    .mySwiper {
        height: 300px;
    }

    .info h3 {
        font-size: 20px;
    }

    .price {
        font-size: 16px;
    }

    .description {
        font-size: 12px;
    }
}
</style>