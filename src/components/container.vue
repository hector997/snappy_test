<template class="container">
    <div class="container px-3 py-5 has-background-white-ter">
        <nav class="level">
            <p class="is-size-4 pl-1 has-text-weight-bold has-text-grey">MY TEAMS </p>
            <button class="level button is-primary" @click="toggleModal()"> Add team</button>
        </nav>
        <!-- con esto armo las filas con los equipos -->
        <table class="table is-striped is-hoverable is-fullwidth py-0 my-0">
            <thead>
                    <th class="pl-6">Teams</th>
                    <th class="is-narrow" title="stores">Stores</th>
                    <th class="is-narrow" title="button1"></th>
                    <th class="is-narrow" title="button2"></th>
            </thead>
            <team />
        </table> 

        <!-- esto es el modal con el form. lo pongo aca para sacar el tema de pasar datos entre componentes ahora. despues armar otro componente con esto -->
        
        <div class="modal" :class="classname" >
            <div class="modal-background" id="bg" ></div>
            <div class="modal-card has-background-withe py-5 px-5" id="modal">

                <header class="modal-card-head">
                    <p class="modal-card-title">Add team</p>
                    <button class="delete is-small" @click="toggleModal()">x</button><!-- este es el botoncito para cerrar -->
                </header>
            
                <section class="modal-card-body">
                    <form @submit.prevent="newTeam()"> <!-- aca llama a la funcion con el emit -->
                        <label class="label">Team Name</label>
                        <div class="field">
                            <p class="control has-icons-left">
                                <input class="input" v-model="nombre" type="text" name="nombre" placeholder="Give a name to your team">
                                <span class="icon is-small is-left">
                                    <i class="fas fa-users"></i>
                                </span>
                            </p>
                        </div>

                        <label class="label" >Users</label>
                        <div class="divardo">
                        <div class="field">
                            <p class="control has-icons-left">
                                <input class="input" type="text" v-model="tempUser" @keyup="addUser" placeholder="Enter each name separated by a' , '. Click on the tags to delete">
                                <span class="icon is-small is-left">
                                       <i class="fas fa-portrait"></i>
                                </span>
                            </p>
                        </div>
                        <!-- aca hago lo del array aux para que quede canchero el form. esto despues lo tengo que meter en 'users' -->
                            <div v-for="user in usersAux" :key="user" class="level tag mx-1 my-1">
                                <span class="icon is-small is-left has-text-primary"><i class="fas fa-circle"></i></span>
                                <a @click="deleteTag(user)" class="has-text-black">{{user}}</a>
                            </div>
                        </div>

                         <label class="label pt-3">Stores</label>
                        <div class="field">
                            <div class="control has-icons-left">
                                <div class="select">
                                <select v-model="stores" type="number" name="stores" placeholder="0">
                                    <option>0</option>
                                    <option>1</option>
                                    <option>2</option>
                                    <option>3</option>
                                    <option>4</option>
                                    <option>5</option>
                                </select>
                                </div>
                                <span class="icon is-small is-left">
                                    <i class="fas fa-store"></i>
                                </span>
                            </div>
                        </div>
                        <!-- este boton tambien llama al submit de arriba -->
                        <button class="submit button is-primary my-2"><i class="fas fa-check"></i></button>
                    </form>
                </section>
                
            </div>
        </div>
    </div>
</template>

<script>

import team from './team.vue';

export default {
    name: 'container',

    data(){
        return{

            isOpen: false,
            newTeamsArr:[],
            nombre:'',
            stores:'',
            tempUser:'',
            usersAux: [],
            test: ' ',
            
        }
    },
    components: {
        team,
    },
    methods:{
        //abre el modal
        toggleModal: function(){
            console.log('went in toggleModal')
            this.tempUser ='',
            this.isOpen = !this.isOpen;
        },
        //suma usuarios al array aux del form para despues meterlos en el objeto 'users'
        addUser(e){
            if(e.key === ',' && this.tempUser){
                if(!this.usersAux.includes(this.tempUser)){
                    this.usersAux.push(this.tempUser)
                }
                this.tempUser = ''
            }
        },
        //borra los usuarios filtrandolos
        deleteTag(user){
            this.usersAux = this.usersAux.filter((i)=>{
                return user !== i
            })
        },
        //funcion para pasar los datos del form al parent
        newTeam:function(){
            this.test = 'anda';
            console.log("onchild: " + this.test)
            
            this.$emit('sent',this.test)
            //const team2= {
              //  Id: Math.random(),
                //nombre: this.nombre,
                //stores: this.stores,
                //users:this.usersAux
            //}
            //this.newTeamsArr.push(this.team2)

            this.isOpen =! this.isOpen // esto cierra el modal
            return
        },
    },
    
    computed: {
        classname: function(){
            return{
                'is-active': this.isOpen //mas cosas para abrir el modal
                }
        }
    }

}
</script>

<style scoped>
    .container{
        background: #fff;
    }

    .is-active .modal{
        max-height: 0%;
    }
    .modal{
        max-height: 100%;
    }
    
</style>
