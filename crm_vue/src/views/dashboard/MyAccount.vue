<template>
    <div class="container">
        <div class="columns is-multiline">
            <div class="column is-12">
                <h1 class="title">My Account</h1>
            </div>

            <div class="column is-12">
                <button @click="logOut()" class="button is-danger">Log out</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'MyAccount',
    methods: {
        async logOut() {
            await axios
                .post('/api/v1/token/logout/')
                .then(response => {
                    console.log('Logged out successfully')
                })
                .catch(error => {
                    console.log(JSON.stringify(error))
                })
            
            axios.defaults.headers.common['Authorization'] = ''
            localStorage.removeItem('token')
            this.$store.commit('removeToken')
            
            this.$router.push('/log-in')
        }
    }
}
</script>