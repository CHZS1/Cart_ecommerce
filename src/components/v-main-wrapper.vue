<template>
    <div class="v-main-wrapper">
        <keep-alive>
            <router-view></router-view>
        </keep-alive>
    </div>    
</template>

<script>


export default {
    name: 'v-main-wrapper',
    props: {},
    data() {
        return {
            title: 'Main wrapper'
        }
    },
    computed: {}
}

</script>

<style>
    .v-main-wrapper {
       max-width: 1360px;
       padding-left: 80px;
       padding-right: 80px;
       margin: 0 auto;
    }

</style>