<template>
    <div class="container">
        <header-view></header-view>
        <div class="row">
            <div class="col md-12">
                <transition name="animation" mode="out-in">
        <router-view></router-view>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
import Header from './components/Header'

export default {
    components: {
        'header-view': Header
    },
    created(){
        this.$store.dispatch('initStocks')
    }
}
</script>

<style>
    body {
        padding: 30px,
    }
    .animation-enter-active{
        animation: slide-in 200ms ease-out forwards

    }
    .animation-leave-active{
        animation: slide-out 200ms ease-out forwards
    }
    @keyframes slide-in {
        from {
        opacity: 0;
        transform: translateY(-30px)
        }
        to{
            transform: translateY(0);
            opacity: 1;

        }
    }
    @keyframes slide-out {
        from {
        opacity: 1;
        transform: translateY(0)
        }
        to{
            transform: translateY(-30);
            opacity: 0;
        }
    }
</style>