<template>
    <div id="app" :class = "['container md-3']">
        <h1 :class="['display-1']">{{texto}}</h1>
        <form>
            <div :class="['form-group']">
                <label for="firstName">First Name</label>
                <input :class="['form-control']" type="text" v-model="firstName">
                <label for="lastName">Last Name</label>
                <input :class="['form-control']" type="text" v-model="lastName">
                <label for="username">Username</label>
                <input :class="['form-control']" type="text" v-model="username">
                <label for="password">Password</label>
                <input :class="['form-control']" type="text" v-model="password">
            </div>
        </form>
        <div :class="['row justify-content-center']">
            <div :class="['col-3']">
                <button :class="['btn btn-primary']" @click="postREST">Registrar con REST</button>
            </div>
            <div :class="['col-3']">
                    <button :class="['btn btn-primary']" @click="postGraphQL">Reguitrar con GraphQL</button>
            </div>
        </div>
        <div v-if="respuesta" :class="[fondoRespuesta, 'row align-items-center']">
            {{textoRespuesta}}
        </div>
    </div>
</template>


<script>
    import gql from 'graphql-tag'
    export default {
        name: 'app',
        data(){
            return {
                firstName: '',
                lastName: '',
                username: '',
                password: ''
            }
        },
        apollo: {
        contacts: gql`query {
        contacts {
            firstName,
            lastName,
            username,
            password
        }
        }`,
        },
        methods: {
            postGraphQL(firstName, lastName, username, password){
            this.$apollo.mutate({
                mutation: gql`mutation postGraphQL($firstName: String!, $lastName: String!, $username: String!, $password: String!){
                    createContact(firstName: $firstName, lastName: $lastName, $username: $username!, $password: $password) {
                        firstName,
                        lastName,
                        username,
                        password
                    }
                }`,
                variables:{
                    firstName: firstName,
                    lastName: lastName,
                    username: username,
                    password: password
                }
            })
            location.reload();
            }
        }
    }
</script>