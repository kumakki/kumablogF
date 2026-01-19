<template>
    <button>
        <slot />
    </button>
</template>

<style scoped lang="scss">
button{
    padding: 10px 20px;
    background-color: transparent;
    color: black;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;

    &:hover {
        background-color: lightgray;
    }
}
</style>