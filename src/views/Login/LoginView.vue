<!-- 登录页面 -->
<template>
    <div class="login-container">
        <div class="login-header">
            <h1>登录</h1>
        </div>
        <div class="login-form">
            <el-form :model="loginForm" :rules="loginRules" ref="loginForm" label-width="80px">
                <el-form-item label="用户名" prop="username">
                    <el-input v-model="loginForm.username" placeholder="请输入用户名"></el-input>
                </el-form-item>
                <el-form-item label="密码" prop="password">
                    <el-input type="password" v-model="loginForm.password" placeholder="请输入密码"></el-input>
                </el-form-item>
                <el-form-item>
                    <el-button type="primary" @click="handleLogin">登录</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script setup>
// import { login } from '@/api/login'
import { ref } from 'vue'

const loginForm = ref({
    username: '',
    password: ''
})

const loginRules = {
    username: [
        { required: true, message: '请输入用户名', trigger: 'blur' },
        { min: 5, max: 20, message: '用户名长度在5到20个字符', trigger: 'blur' }
    ],
    password: [
        { required: true, message: '请输入密码', trigger: 'blur' },
        { min: 6, max: 20, message: '密码长度在6到20个字符', trigger: 'blur' }
    ]
}

const handleLogin = () => {
    $refs.loginForm.value.validate((valid) => {
        if (valid) {
            login(loginForm).then(response => {
                console.log(response)
            }).catch(error => {
                console.log(error)
            })
        } else {
            console.log('error submit')
        }
    })
}
</script>


<style scoped>
.login-container {
    width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
}

.login-header {
    text-align: center;
    margin-bottom: 20px;
}

.login-form {
    width: 100%;
}
</style>