<template>
    <div class="header">
        <div>
            <BaseLinkButton @click="onClickTitle">My Blog</BaseLinkButton>
        </div>
        <div class="right">
        </div>
    </div>
</template>

<script setup lang="ts">
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