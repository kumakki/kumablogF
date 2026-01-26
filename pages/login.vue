<template>
    <div class="login">
        <h2>a</h2>
        <div class="line">
            <span class="content">メールアドレスまたはユーザーID</span>
            <BaseInputBox class="textbox" placeholder="例）xxx@xxxmail.com" v-model="emailOrUserId" />
        </div>
        <p>{{ errorEmailOrUserId }} </p>
        <div class="line">
            <span class="content">パスワード</span>
            <BaseInputBox class="textbox" type="password" placeholder="パスワードを入力" v-model="password" />
        </div>
        <p>{{ errorPassword }} </p>
        <BaseOutlineButton @click="onClickRegister">ログイン</BaseOutlineButton>
        <p> </p>>
    </div>
</template>

<script setup>
definePageMeta({
    layout: 'auth'
})
const route = useRoute();
const redirect = route.query.redirect ?? "/";


const config = useRuntimeConfig();
const base = config.public.apiBase;

const errorEmailOrUserId = ref("");
const errorPassword = ref("");

const emailOrUserId = ref("");
const password = ref("");

const onClickRegister = async () => {

    if (emailOrUserId.value === "") {
        errorEmailOrUserId.value = "メールアドレスまたはユーザーIDを入力してください";
        return;
    }
    if (password.value === "") {
        errorPassword.value = "パスワードを入力してください";
        return;
    }

    const registerData = {
        emailOrUserId: emailOrUserId.value,
        password: password.value,
    };

    try {
        const response = await $fetch(`${base}/auth/login`, {
            method: "POST",
            body: registerData,
            credentials: "include"
        });

        // 成功
        navigateTo(redirect);

    } catch (err) {
        // ここにサーバーのエラーが入る
        const errors = err.data?.data;

        errorEmailOrUserId.value = errors?.errorEmailOrUserId ?? "";
        errorPassword.value = errors?.errorPassword ?? "";
    }
}





</script>

<style scoped lang="scss">
.login {
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 80vh;
}

.line {
    display: flex;
    flex-direction: row;
    justify-content: center;
    margin: 10px;
    width: 650px;
}

.content {
    width: 300px;
    margin-top: 10px;
}

.textbox {
    width: 350px;
}
</style>