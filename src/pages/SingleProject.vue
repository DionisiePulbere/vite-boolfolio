<script>
import axios from 'axios';
import Loader from '../components/Loader.vue';
import { store } from '../store.js';

export default {
    name: 'SingleProject',
    components:{
        Loader
    },
    data() {
        return {
            store,
            project: null,
            loading: true
        };
    },
    methods: {
        getProjectDetails() {
            this.loading = true;

            axios.get(`${this.store.apiBaseUrl}/api/projects/${this.$route.params.slug}`)
            .then((response) => {
                this.project = response.data.project;

                this.loading = false;
            });
        }
    },
    mounted() {
        this.getProjectDetails();
    }
}

</script>

<template>
    <div class="container">
        <div v-if="!loading">
            <div v-if="project">
                <h1>{{ project.name }}</h1>
                <div v-if="project.type">
                    <p><strong>Type</strong>: {{ project.type.name }}</p>
                </div>
                <div v-if="project.technologies.length > 0">
                    <strong>Technologies</strong>: 
                    <span>
                        <div v-for="technology in project.technologies" class="badge rounded-pill text-bg-success mx-1">{{ technology.name }}</div>
                    </span>
                </div>

                <p><strong>Summary</strong>: {{ project.summary }}</p>
            </div>
        </div>
        <div v-else>
            <Loader></Loader>
        </div>
    </div>
</template>


<style scoped lang="scss">

</style>