<template>
    <div>
        <LoginPage v-if="page == 'login-page'">
        </LoginPage>
        <RegisterPage v-else-if="page == 'register-page'"></RegisterPage>
        <HomePage v-else-if="page == 'home-page'"></HomePage>
    </div>
</template>

<script>
import HomePage from './components/HomePage';
import LoginPage from './components/LoginPage';
import RegisterPage from './components/Register';
export default {
    name: 'App',
    data(){
        return {
        page: 'home-page',
        show: false,
        showEdit: false,
        server: 'http://localhost:3000',
        tasks: '',
        taskAdd: {
            title: ''
        },
        getTaskById: {
            id: '',
            title: ''
        },
        errorMessage: '' 
        }
    },
    components: {
        HomePage,
        LoginPage,
        RegisterPage
    },
    methods: {
        changePage(name) {
            this.page = name;
        }
    }
}
</script>
    
<style>

</style>