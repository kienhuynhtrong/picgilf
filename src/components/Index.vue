<template>
    <div>
        <div class="loader" v-if="isLoading">
            <Loader :isShow="isLoading" />
        </div>
        <div class="wrap-content">
            <div class="container">
                <div class="row">
                    <div v-for="(item, idx ) in data" :key="idx" 
                    class="contentImg col-lg-3 col-sm-4 col-xs-6">
                        <img 
                        :key="idx"
                        class="item"
                        :src="item.images.fixed_width.url"
                    >
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>
<script>
import axios  from 'axios';
import Loader from '../components/Loader/Loader'
export default {
    name:'Index',
    data: ()=>({
        urlEndpoint:'https://api.giphy.com/v1/gifs/trending',
        isLoading:false,
        data:[],
    }),
    components: {
        Loader,
    },
    computed: {

    },
    created() {
        this.getDataImage()
    },
    methods: {
        async getDataImage() {
            this.isLoading = true
            try {
                const { data } = await axios.get(this.urlEndpoint, {
                    params : {
                api_key: '1UWI1RQmL1Dbe96nFhuNNnkMdyUnwTNS',
                limit: 20,
                offset: 5,
                rating: 'g',
                random_id: 'e826c9fc5c929e0d6c6d423841a282aa'
            }
                });
                this.data = data.data
            } catch(error){
                return false
            } finally {
                this.isLoading = false
            }
        }
    }
}
</script>
<style lang='scss' src='./index.scss'>
</style>