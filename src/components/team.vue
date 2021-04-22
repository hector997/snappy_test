<template>
        <tbody>
            <tr v-for="team in teamsArr" :key="team.id">
                <td class="teamName" :class="accordionClasses" @click="toggleAccordion()" >
                    <span class="arrow" ><i class="fas fa-angle-right px-3 has-text-info"></i></span>
                    <a class="nombre has-text-black">{{team.nombre}}</a>
                    <div class="content">
                        <div class="card">
                                <p>card</p>
                        </div>
                    </div>
                    </td>
                <td><span class="tag ml-3 is-info"> {{team.stores}} </span></td>
                <td><span class="icon has-text-grey"><i class="fas fa-pen"></i></span></td>
                <td><span class="icon has-text-grey deleteButton " @click="deleteTeam(team)"><i class="fas fa-trash-alt"></i></span></td>
            </tr>
        </tbody>
</template>

<script>
export default {
    data(){
        return{
        isOpen: true,
        teamsArr: [],
        }

    },
    mounted(){
         fetch('http://localhost:3000/teams')
        .then(response => response.json())
        .then(data => this.teamsArr = data)
        .catch(err => console.log(err.message))
    },
    methods: {
        toggleAccordion: function(){
            this.isOpen = !this.isOpen;
            
        },
        deleteTeam:function(team) {
            console.log(this.teamsArr)

            this.teamsArr = this.teamsArr.filter((i) =>{
                return team !== i
            })
            console.log(this.teamsArr)

        }
    },
    computed: {
        accordionClasses: function(){
            return{
                'is-closed': this.isOpen
                }
        }
    }
}

</script>
<style scoped>
    .card {
        max-width: 100px;
    }
    .content {
        padding: 0;
        max-height: 20em;
        overflow: hidden;
        transition: 0.3s ease all;
    }
    .is-closed .content{
        max-height: 0;
    }
    
    .icon{
        cursor: pointer;
    }
    .icon:hover{
        transition: 0.2s;
        text-shadow: 2px 2px 4px rgb(145, 145, 145);
    }
</style>

