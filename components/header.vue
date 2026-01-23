<template>
    <div class="header">
        <div class="left">
            <BaseLinkButton @click="onClickTitle">My Blog</BaseLinkButton>
        </div>
        <div class="right">
            <BaseOutlineButton>My Accounts</BaseOutlineButton>
        </div>
    </div>
</template>

<script setup lang="ts">
    //クリック処理
    const onClickTitle = () => {
        navigateTo('/');
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