<script>
import axios from 'axios';
import { store } from '../store.js';
import SingleProject from '../components/SingleProject.vue';
import Loader from '../components/Loader.vue';

export default {
    name: 'ProjectList',
    components: {
        SingleProject,
        Loader
    },
    data() {
        return {
            store,
            projects: [],
            currentPage: 1,
            prevPageUrl: null,
            nextPageUrl: null,
            lastPage: 0,
            isLoading: false
        }
    },
    methods: {
        getProjects(pageNumber) {
            this.isLoading = true;
            axios.get(`${this.store.baseApiUrl}/api/projects`, {
                params: {
                    page: pageNumber
                }
            })
                .then((response) => {
                    if (response.data.success) {
                        this.projects = response.data.results.data;
                        this.currentPage = response.data.results.current_page;
                        this.prevPageUrl = response.data.results.prev_page_url;
                        this.nextPageUrl = response.data.results.next_page_url;
                        this.lastPage = response.data.results.last_page;

                        this.isLoading = false;
                    } else {
                        this.$router.push({ name: 'not-found' });
                    }
                });
        }
    },
    mounted() {
        this.getProjects(this.currentPage);
    }

}
</script>

<template>
    <div class="container my-3">
        <div v-if="!isLoading" class="row row-cols-3">
            <template v-if="projects">
                <div class="col my-3" v-for="project in projects">
                    <SingleProject :projectDetails="project" :key="project.id"></SingleProject>
                </div>
            </template>
        </div>
        <template v-else>
            <Loader></Loader>
        </template>

        <!-- pagination  -->
        <template v-if="projects && !isLoading">
            <nav aria-label="pagination">
                <ul class="pagination justify-content-center pt-3">
                    <li class="page-item " :class="[prevPageUrl == null ? 'disabled' : '']">
                        <a @click="getProjects(currentPage - 1)" class="page-link">Previous</a>
                    </li>

                    <li v-for="n in lastPage" class="page-item" :class="[currentPage == n ? 'active' : '']"
                        aria-current="page">
                        <a @click="getProjects(n)" class="page-link">{{ n }}</a>
                    </li>

                    <li class="page-item" :class="[nextPageUrl == null ? 'disabled' : '']">
                        <a @click="getProjects(currentPage + 1)" class="page-link">Next</a>
                    </li>
                </ul>
            </nav>
        </template>
    </div>
</template>
