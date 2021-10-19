<template>
    <div class="pa-2">
    <div class="text-h4 text-center">
        TEMPLATE EDITAR
    </div>
    <v-form
            ref="form"
            lazy-validation
            class="pa-10"
        >
        <v-text-field
            v-model="name"
            :counter="10"
            :rules="nameRules"
            label="Name"
            required
        ></v-text-field>

        <v-text-field
            v-model="email"
            :rules="emailRules"
            label="E-mail"
            required
        ></v-text-field>

        <v-btn
            color="success"
            class="mr-4"
            @click="modificarUsuario"
        >
            <v-icon left>
                mdi-content-save
            </v-icon>
             Edit User
        </v-btn>

        <v-btn
            color="error"
            class="mr-4"
            @click="goHome"
        >
            <v-icon left>
                mdi-eraser-variant
            </v-icon>
            Go Home
        </v-btn>
        </v-form>
    </div>
</template>
<script>
    export default {
        data: () => ({
        name: '',
        nameRules: [
        v => !!v || 'Name is required',
        v => (v && v.length <= 10) || 'Name must be less than 10 characters',
        ],
        email: '',
        emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+\..+/.test(v) || 'E-mail must be valid',
        ],
        usuario: {}
}),

methods: {
        goHome () {
            window.location.href('/listar')
        },
        modificarUsuario(){
            

        },
        obtenerUsuario(){
            console.log(this.idUsuario)
        }
    },
    mounted() {
        this.obtenerUsuario()
    },
    computed: {
        idUsuario: {
            get(){
                return this.$store.state.idUsuario
            }
        }
    }
}
</script>