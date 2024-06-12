<script>
import axios from 'axios';
import { store } from '../store.js';
import Loader from '../components/Loader.vue';

export default {
    name: 'ProjectDetails',
    components: {
        Loader
    },
    data() {
        return {
            store,
            project: null,
            isLoading: false
        }
    },
    methods: {
        getProjectDetails() {
            this.isLoading = true;
            axios.get(`${this.store.baseApiUrl}/api/projects/${this.$route.params.slug}`)
                .then((response) => {
                    if (response.data.success) {
                        this.project = response.data.results;
                        this.isLoading = false;
                    } else {
                        this.$router.push({ name: 'not-found' });
                    }
                });
        },
        changeTechBadgeColor(technologyName) {
            return {
                'text-bg-primary': technologyName == 'css',
                'text-bg-warning': technologyName == 'js',
                'text-bg-success': technologyName == 'vue',
                'text-bg-secondary': technologyName == 'sql',
                'text-bg-dark': technologyName == 'php',
                'text-bg-danger': technologyName == 'laravel',
            }
        },
    },
    mounted() {
        this.getProjectDetails();
    }
}
</script>

<template>
    <div class="container my-3">
        <div v-if="!isLoading" class="row">
            <template v-if="project">
                <div class="card h-100">
                    <div class="card-body">
                        <h5 class="card-title fw-bold">{{ project.name }}</h5>

                        <div><span class="fw-bold">Client: </span>{{ project.client_name }}</div>

                        <div v-if="project.type"><span class="fw-bold">Type: </span>{{ project.type.name
                            }}</div>

                        <template v-if="project.technologies.length > 0">
                            <div class="fw-bold mb-1">Technologies:</div>
                            <div class="d-flex flex-wrap gap-1">
                                <div v-for="technology in project.technologies" class="badge"
                                    :class="changeTechBadgeColor(technology.name)">
                                    {{ technology.name }}
                                </div>

                            </div>
                        </template>

                        <p class="mt-2">{{ project.summary }}</p>

                        <div v-if="project.cover_image" class="w-75 m-auto">
                            <img :src="`${this.store.baseApiUrl}/storage/${project.cover_image}`"
                                class="card-img-bottom img-fluid" :alt="project.name">
                        </div>
                    </div>
                </div>
            </template>
        </div>
        <template v-else>
            <Loader></Loader>
        </template>
    </div>
</template>