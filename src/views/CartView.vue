<template>
    <div class="col-md-4">
      <h2 class="mb-3">購物車</h2>
      <div v-if="carts.length === 0">購物車是空的</div>
      <ul class="list-group mb-3">
        <li v-for="item in carts" :key="item.id" class="list-group-item d-flex justify-content-between align-items-center">
          <div>
            <h6 class="my-0">{{ item.name }}</h6>
            <small class="text-muted">數量：{{ item.quantity }}</small>
          </div>
          <div>
            <span class="text-muted">${{ item.price * item.quantity }}</span>
            <button class="btn btn-sm btn-outline-danger ms-2" @click="handleRemoveCart(item)"> 移除 </button>
          </div>
        </li>
      </ul>
       <!-- 合計金額區塊 -->
    <div v-if="carts.length > 0" class="text-end fw-bold">
      合計金額：${{ totalPrice }}
    </div>
    </div>
    
 
</template>

<script setup>
import { inject, computed } from 'vue';

  const props = defineProps({
    carts: {
      type: Array,
      required: true
    }
  });

  const emit = defineEmits(['remove-cart']);
  const showNotification = inject('showNotification');
  const handleRemoveCart = (item) => {
    emit('remove-cart', item);
    showNotification(`${item.name} 已從購物車移除`, 'danger');
  }

  // 計算合計金額
const totalPrice = computed(() => {
  return props.carts.reduce((sum, item) => sum + item.price * item.quantity, 0);
});

</script>