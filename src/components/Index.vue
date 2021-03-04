<template>
    <div>
        <div class="loader" v-if="isLoading">
            <Loader :isShow="isLoading" />
        </div>
        <div class="wrap-content">
            <h3 class="wrap-content__titie text-center">List Image</h3>
            <div class="container">
                <div class="row">
                    <div v-for="(item, idx ) in data" :key="idx" 
                    class="contentImg col-lg-3 col-sm-4 col-xs-6">
                        <img
                        @click="openModal(item)"
                        :key="idx"
                        class="item"
                        :src="item.images.fixed_width.url"
                    >
                    </div>
                </div>
                <div class="wrap-content__load-more text-center">
                    <button class="text-center" @click="showMore()">Load More</button>
                </div>
            </div>

        </div>
        <Modal v-if="showModal" 
        :src="linkUrl" 
        @close="closeModal()"></Modal>
    </div>
</template>
<script>
import axios  from 'axios';
import Loader from '../components/Loader/Loader'
import Modal from '../components/Modal/Modal'
export default {
    name:'Index',
    data: ()=>({
        urlEndpoint:'https://api.giphy.com/v1/gifs/trending',
        isLoading:false,
        data:[],
        limit: 24,
        linkUrl:'',
        showModal: false
    }),
    components: {
        Loader,Modal
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
                limit: this.limit,
                offset: 5,
                rating: 'g',
                random_id: 'e826c9fc5c929e0d6c6d423841a282aa'
            }
                });
                this.data = data.data
                this.isLoading = false
            } catch(error){
                return false
            }
        },

        showMore() {
            this.limit = this.limit +24;
            this.getDataImage();
        },

        openModal(item) {
            this.showModal = true
            this.linkUrl = item.images.fixed_width.url
        },

        closeModal() {
            this.showModal = false
        }
    }
}
</script>
<style lang='scss' src='./index.scss'>
</style>