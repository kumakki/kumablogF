<template>
    <div class="login">
        <h2>a</h2>
        <div class="line">
            <span class="content">メールアドレス</span>
            <BaseInputBox class="textbox" placeholder="例）xxx@xxxmail.com" v-model="email" />
        </div>
        <p>{{ errorEmail }} </p>
        <div class="line">
            <span class="content">ユーザーID</span>
            <BaseInputBox class="textbox" placeholder="例）abcd_1234" v-model="userId" />
        </div>
        <p>{{ errorUserId }} </p>
        <div class="line">
            <span class="content">ユーザー名</span>
            <BaseInputBox class="textbox" placeholder="例）山田 太郎" v-model="userName" />
        </div>
        <p>{{ errorUserName }} </p>
        <div class="line">
            <span class="content">パスワード</span>
            <BaseInputBox class="textbox" type="password" placeholder="パスワードを入力" v-model="password" />
        </div>
        <p>{{ errorPassword }} </p>
        <div class="line">
            <span class="content">パスワードの確認</span>
            <BaseInputBox class="textbox" type="password" placeholder="パスワードをもう一度入力" v-model="passwordConfirm" />
        </div>
        <p>{{ errorPasswordConfirm }} </p>
        <BaseOutlineButton @click="onClickRegister">登録</BaseOutlineButton>
        <p> </p>>
    </div>
</template>

<script setup>
definePageMeta({
    layout: 'auth'
})

const config = useRuntimeConfig()
const base = config.public.apiBase

const errorEmail = ref("");
const errorUserId = ref("");
const errorUserName = ref("");
const errorPassword = ref("");
const errorPasswordConfirm = ref("");

const email = ref("");
const userId = ref("");
const userName = ref("");
const password = ref("");
const passwordConfirm = ref("");

const onClickRegister = async () => {

    if (email.value === "") {
        errorEmail.value = "メールアドレスを入力してください";
        return;
    }
    if (userId.value === "") {
        errorUserId.value = "ユーザーIDを入力してください";
        return;
    }
    if (userName.value === "") {
        errorUserName.value = "ユーザー名を入力してください";
        return;
    }
    if (password.value === "") {
        errorPassword.value = "パスワードを入力してください";
        return;
    }
    if (passwordConfirm.value === "") {
        errorPasswordConfirm.value = "パスワードの確認を入力してください";
        return;
    }
    if (password.value !== passwordConfirm.value) {
        errorPasswordConfirm.value = "パスワードが一致しません";
        return;
    }

    const registerData = {
        email: email.value,
        userId: userId.value,
        username: userName.value,
        password: password.value,
    };

    const response = await $fetch(`${base}/users`, {
        method: "POST",
        body: registerData,
        credentials: "include"
    });


    if (response.success === true) {
        navigateTo("/profile");
    } else {
        errorEmail.value = response.data.errorEmail;
        errorUserId.value = response.data.errorUserId;
        errorUserName.value = response.data.errorUserName;
        errorPassword.value = response.data.errorPassword;
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
    width: 500px;
}

.content {
    width: 150px;
    margin-top: 10px;
}

.textbox {
    width: 350px;
}
</style>