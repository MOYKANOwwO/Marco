<template>
    <div class="pa-2">
        <div class="text-h4 text-center">
            Usuarios del Sistema
        </div>
        <div class="pa-3">
            <v-data-table :headers="headers" :items-per-page="10" :items="usuariosBD" class="elevation-5">
                <template #[`item.editar`]="{ item }">
                    <v-btn color="indigo lighten-4" fab x-small @click="editarUsuario(item.id)">
                        <v-icon>
                            mdi-account-edit
                        </v-icon>
                    </v-btn>
                </template>
                <template #[`item.borrar`]="{ item }">
                    <v-btn color="red lighten-4" fab x-small @click="guardarUsuario(item.id)">
                        <v-icon>
                            mdi-trash-can
                        </v-icon>
                    </v-btn>
                </template>
            </v-data-table>

                <v-dialog
                    v-model="dialog"
                    persistent
                    max-width="290"
                >
            <v-card>
                <v-card-title class="text-h5" style="background: blue; color: white;">
                    Users Crud
            </v-card-title>
            <v-card-text>Are you shure you want to delete the user?</v-card-text>
                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="green darken-1"
                    text
                    @click="dialog = false"
                >
                    Cancelar
                </v-btn>
                <v-btn
                    color="red darken-1"
                    text
                    @click="borrarUsuario(usuarioId)"
                >
                        Borrar
                    </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </div>
</div>
</template>

<script>
import vuex from 'vuex'

export default {
    data(){
        return{
            usuariosBD: [],
            headers: [
                {text: 'ID', value: 'id', align: 'center', sortable: false},
                {text: 'NOMBRE', value: 'nombre', align: 'center', sortable: false},
                {text: 'CORREO', value: 'correo', align: 'center', sortable: false},
                {text: 'EDITAR', value: 'editar', align: 'center', sortable: false},
                {text: 'BORRAR', value: 'borrar', align: 'center', sortable: false},
            ],
            itemsBD: [],
            dialog: false,
        }
    },
    created: function(){
        this.consultarUsuarios()
    },
    methods: {
        consultarUsuarios(){
            fetch('http://localhost:8888/')
            .then(respuesta => respuesta.json())
            .then((datosRespuesta) => {
                this.usuariosBD = []
                if(typeof datosRespuesta[0].success === 'undefined'){
                    this.usuariosBD = datosRespuesta
                    this.usuariosBD.forEach( item => {
                        console.log(item)
                    })
                    //console.log(this.usuariosBD)
                }
            })
            .catch(console.log)
        },
        editarUsuario(id){
            this.$store.commit('setIdUsuario', id)
            window.location.href = "/editar"
        },
        borrarUsuario(usuarioId){
            console.log(usuarioId)
            fetch('http://localhost:8888/?borrar='+usuarioId)
            .then( respuesta => respuesta.json)
            .then( (datosRespuesta) =>{
            this.usuarioId = null
            window.location.href = "listar"
            })
        },
        guardarUsuario(id){
            this.usuarioId = id
            this.dialog = true
        }
    }
}
</script>