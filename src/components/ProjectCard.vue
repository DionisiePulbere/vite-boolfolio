<script>
export default{
    name: 'ProjectCard',
    props: {
        projectDetails: Object
    },

}
</script>


<template>
     <div class="col">
        <div class="card my-3">
            <!-- <img src="..." class="card-img-top" alt="..."> -->
            <div class="card-body">
                <h5 class="card-title">{{ projectDetails.name }}</h5>
                <p v-if="projectDetails.summary" class="card-text">{{ projectDetails.summary }}</p>
                <!-- <a href="#" class="btn btn-primary">Go somewhere</a> -->
            </div>
        </div>
    </div>
</template>

<style scoped lang="scss">

</style>