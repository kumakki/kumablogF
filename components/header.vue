<template>
    <div class="header">
        <div class="left">
            <BaseLinkButton @click="onClickTitle">My Blog</BaseLinkButton>
        </div>
        <div class="right">
            <BaseOutlineButton v-if="sessionSuccess" @click="onClickProfile">{{ accountName }}</BaseOutlineButton>
            <BaseOutlineButton v-else @click="onClickLogin">ログイン</BaseOutlineButton>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

const config = useRuntimeConfig()
const base = config.public.apiBase

const sessionSuccess = ref<boolean>(false)
const accountName = ref("")

type SessionResponse = {
  success: boolean
  data: string
}

onMounted(async () => {
    try {
        const response = await $fetch<SessionResponse>(`${base}/auth/session`, {
            credentials: "include"
        })

        sessionSuccess.value = true
        accountName.value = response.data;

    } catch (err: any) {
        sessionSuccess.value = false
    }
})


const onClickTitle = () => {
    navigateTo('/');
};

const onClickLogin = () => {
    navigateTo('/login');
};

const onClickProfile = () => {
    navigateTo('/profile');
};

</script>

<style scoped Lang="scss">
.header {
    display: flex;
    justify-content: space-between;
    /* 左右に分ける */
    align-items: center;
    /* 縦方向を中央揃え */
    padding: 0 20px;
    height: 60px;
    border-bottom: 1px solid gray;
}

.right {
    display: flex;
}
</style>