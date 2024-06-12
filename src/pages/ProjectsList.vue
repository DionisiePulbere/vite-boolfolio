<script>
import axios from 'axios';
import { store } from '../store.js';
import ProjectCard from '../components/ProjectCard.vue';
import Loader from '../components/Loader.vue';

export default{
    name: 'ProjectList',
    components:{
        ProjectCard,
        Loader
    },
    data() {
        return{
            store,
            projects: [],
            currentPage: 1,
            nextPageUrl: null,
            prevPageUrl: null,
            loading: false


        };
    },
    methods: {
        getProjects(dataPage) {
            this.loading = true;

            axios.get(`${this.store.apiBaseUrl}/api/projects`, {
                params: {
                    page: dataPage
                }
            })
                .then((response) => {
                    this.projects = response.data.results.data;
                    this.currentPage = response.data.results.current_page;
                    this.nextPageUrl = response.data.results.next_page_url; 
                    this.prevPageUrl = response.data.results.prev_page_url; 

                    this.loading = false;
            });
        }
    },
    mounted() {
        this.getProjects(this.currentPage);
    }
}
</script>

<template>
    <div class="container">
        <h1 class="text-center">Tutti i Progetti</h1>
        <div v-if="!loading" class="row row-cols-3">
            <div class="col" v-for="project in projects" :key="project.id">
                <ProjectCard :projectDetails="project"></ProjectCard>
            </div>
        </div>
        <div v-else>
            <Loader></Loader>
        </div>
        <nav aria-label="Page navigation example ">
            <ul class="pagination d-flex justify-content-center">
                <li class="page-item" v-if="prevPageUrl">
                    <a class="page-link" @click="getProjects(currentPage - 1)">Previous</a>
                </li>
                <li class="page-item" v-if="nextPageUrl">
                    <a class="page-link" @click="getProjects(currentPage + 1)">Next</a>
                </li>
            </ul>
        </nav>
    </div>
</template>

<script scoped lang="scss">

</script>