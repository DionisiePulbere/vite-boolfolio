<script>
export default{
    name: 'ProjectCard',
    props: {
        projectDetails: Object
    },
    methods: {
        truncateText(text) {
            if(text.length > 100) {
                return text.substr(0, 99) + '...';
            }

            return text;
        }
    }
}
</script>


<template>
     <div class="col">
        <div class="card my-3">
            <!-- <img src="..." class="card-img-top" alt="..."> -->
            <div class="card-body">
                <h5 class="card-title">{{ projectDetails.name }}</h5>
                <div v-if="projectDetails.type">
                    <strong>Type</strong>: {{ projectDetails.type.name }} 
                </div>
                <div v-if="projectDetails.technologies.length > 0">
                    <strong>Technology</strong>: <span v-for="technology in projectDetails.technologies">{{ technology.name }} &nbsp;</span>
                </div>
                <p v-if="projectDetails.summary" class="card-text">{{ truncateText(projectDetails.summary) }}</p>
                <router-link :to="{ name: 'single-project', params: { slug: projectDetails.slug } }" class="btn btn-primary">Show More</router-link>
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">
.card{
    height: 240px;
}

</style>