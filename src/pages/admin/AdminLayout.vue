<template>
    <div class="overflow-hidden">
        <MyHeader/>
        <main>
        <router-view></router-view>
        </main>
        <MyFooter></MyFooter>
    </div>
</template>

<script>
import MyFooter from '../../components/MyFooter.vue'
import MyHeader from '../../components/MyHeader.vue'
export default{
    name:'MyLayout',
    components:{
        MyFooter,
        MyHeader,        
    }
}
</script>