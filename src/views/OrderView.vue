<script>
export default {
    data() {
        return {
            formData: {
                name: '',
                phone: '',
                address: '',
                productName: '',
                quantity: 1,
            },
            errors: {
                name: '',
                phone: '',
                address: '',
            },
            product: null,
        }
    },
    created() {
        const productData = localStorage.getItem('product');
        if (productData) {
            this.product = JSON.parse(productData);
            // 自動填入產品名稱
            this.formData.productName = this.product.name;
        }
    },
    methods: {
        increaseQuantity() {
            this.formData.quantity++;
        },
        decreaseQuantity() {
            if (this.formData.quantity > 1) {
                this.formData.quantity--;
            }
        },
        // 表單驗證
        validateForm() {
            let isValid = true;
            this.errors = {
                name: '',
                phone: '',
                address: '',
                quantity: '',
            };
            if (!this.formData.name.trim()) {
                this.errors.name = '請輸入姓名';
                isValid = false;
            }
            if (!this.formData.phone.trim()) {
                this.errors.phone = '請輸入電話號碼';
                isValid = false;
            } else if (!/^09\d{8}$/.test(this.formData.phone)) {
                this.errors.phone = '請輸入正確的手機號碼格式';
                isValid = false;
            }
            if (!this.formData.address.trim()) {
                this.errors.address = '請輸入地址';
                isValid = false;
            }
            if (this.formData.quantity < 1) {
                this.errors.quantity = '數量必須大於0';
                isValid = false;
            }

            return isValid;
        },
        // 提交表單
        submitOrder() {
            if (this.validateForm()) {
                console.log('訂單資料：', this.formData);
                alert('訂購成功！');
                this.$router.push('/');
            }
        },
    },
}
</script>

<template>
    <div class="container">
        <div class="content">
            <h1>訂購表單</h1>
            <img :src="product.photo" :alt="product.name">
            <form @submit.prevent="submitOrder">
                <label>姓名<span class="required">*</span></label>
                <input type="text" v-model="formData.name" class="form-input" placeholder="請輸入姓名" required>
                <span class="error" v-if="errors.name">{{ errors.name }}</span>

                <label>聯絡電話<span class="required">*</span></label>
                <input type="tel" v-model="formData.phone" class="form-input" placeholder="請輸入手機號碼">
                <span class="error" v-if="errors.phone">{{ errors.phone }}</span>

                <label>地址<span class="required">*</span></label>
                <input type="text" v-model="formData.address" class="form-input" placeholder="請輸入地址" required>
                <span class="error" v-if="errors.address">{{ errors.address }}</span>

                <label>產品名稱</label>
                <span class="productName">{{ formData.productName }}</span>

                <label>數量 <span class="required">*</span></label>
                <div class="quantity-input">
                    <button type="button" @click="decreaseQuantity" class="quantity-btn">-</button>
                    <input type="number" v-model.number="formData.quantity" min="1" class="form-input quantity"
                        required>
                    <button type="button" @click="increaseQuantity" class="quantity-btn">+</button>
                </div>
                <span class="error" v-if="errors.quantity">{{ errors.quantity }}</span>

                <div class="button">
                    <button type="submit" class="submit-btn">確認訂購</button>
                    <button type="button" @click="$router.push('/')" class="cancel-btn">
                        取消
                    </button>
                </div>
            </form>
        </div>
    </div>
</template>

<style scoped>
.container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
}

.content {
    background: white;
    padding: 30px;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    color: #333;
    margin-bottom: 30px;
}

label {
    display: flex;
    margin: 20px 0 8px 0;
    font-weight: 600;
    color: #333;
}

img {
    width: 250px;
    height: 250px;
    object-fit: cover;
    border-radius: 4px;
    display: block;
    margin: 0 auto 15px auto;
}

.required {
    color: #dc3545;
}

.form-input {
    width: 100%;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 16px;
    transition: border-color 0.3s;
}

.form-input:focus {
    outline: none;
    border-color: #4CAF50;
    box-shadow: 0 0 0 2px rgba(76, 175, 80, 0.1);
}

.quantity-input {
    display: flex;
    align-items: center;
    gap: 10px;
}

.productName {
    padding: 10px 0;
    font-size: 16px;
}

.quantity {
    width: 80px;
    text-align: center;
}

.quantity-btn {
    width: 32px;
    height: 32px;
    border: 1px solid #ddd;
    background: #f8f9fa;
    border-radius: 4px;
    cursor: pointer;
    font-size: 18px;
    display: flex;
    align-items: center;
    justify-content: center;
}

.quantity-btn:hover {
    background: #e9ecef;
}

.error {
    color: #dc3545;
    font-size: 0.875em;
    margin-top: 5px;
}

.button {
    display: flex;
    gap: 15px;
    margin-top: 30px;
}

.submit-btn,
.cancel-btn {
    flex: 1;
    padding: 12px;
    border: none;
    border-radius: 4px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.submit-btn {
    background: #4CAF50;
    color: white;
}

.submit-btn:hover {
    background: #45a049;
}

.cancel-btn {
    background: #f44336;
    color: white;
}

.cancel-btn:hover {
    background: #da190b;
}
</style>