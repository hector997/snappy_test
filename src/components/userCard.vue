<template>
    <div class="card">
        <div v-for="user in users" :key="user.nombre">
            <div class="card-image">
            </div>
            <div class="media-content">
            <p>{{user.nombre}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'userCard',
    data(){
        return{
            users: [],
        }
    },
}
</script>