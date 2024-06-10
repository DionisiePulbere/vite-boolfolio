<script>
import axios from 'axios';
import ProjectCard from './ProjectCard.vue';

export default{
    name: 'ProjectList',
    components:{
        ProjectCard
    },
    data() {
        return{
            projects: []

        };
    },
    methods: {
        getProjects() {
            axios.get('http://127.0.0.1:8000/api/projects')
                .then((response) => {
                    this.projects = response.data.results;
            });
        }
    },
    mounted() {
        this.getProjects();
    }
}
</script>

<template>
    <div class="container">
        <h1 class="text-center">Tutti i Progetti</h1>
        <div class="row row-cols-3">
            <SingleProject v-for="project in projects" :projectDetails="project" :key="project.id"></SingleProject>
        </div>
    </div>
</template>

<script scoped lang="scss">

</script>