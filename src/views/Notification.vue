<template>
    <div v-if="notificationState.isShow" class="position-fixed top-0 end-0 p-3" style="z-index: 1050">
        <div :class="['toast show align-items-center text-white border-0', bgClass]">
        <div class="d-flex">
            <div class="toast-body">{{ notificationState.message }}</div>
            <button type="button" class="btn-close btn-close-white me-2 m-auto"
            @click="notificationState.isShow = false"
            ></button>
        </div>
        </div>
    </div>
</template>

<script setup>
    import { inject, computed } from 'vue';
    
    const notificationState = inject('notificationState', { isShow: false, message: '' , type: 'success'});
    const showNotification = inject('showNotification', () => {});
    
    const bgClass = computed(() => {
        return notificationState.type === 'success' ? 'bg-success' : 'bg-danger';
    });
</script>