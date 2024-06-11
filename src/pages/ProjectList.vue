<script>
import axios from 'axios';
import SingleProject from '../components/SingleProject.vue';

export default {
    name: 'ProjectList',
    components: {
        SingleProject
    },
    data() {
        return {
            projects: [],
            currentPage: 1,
            prevPageUrl: null,
            nextPageUrl: null,
            lastPage: 0
        }
    },
    methods: {
        getProjects(pageNumber) {
            axios.get('http://127.0.0.1:8000/api/projects', {
                params: {
                    page: pageNumber
                }
            })
                .then((response) => {
                    this.projects = response.data.results.data;
                    this.currentPage = response.data.results.current_page;
                    this.prevPageUrl = response.data.results.prev_page_url;
                    this.nextPageUrl = response.data.results.next_page_url;
                    this.lastPage = response.data.results.last_page;
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
        <div class="row row-cols-3">
            <template v-if="projects">
                <div class="col my-3" v-for="project in projects">
                    <SingleProject :projectDetails="project" :key="project.id"></SingleProject>
                </div>
            </template>
        </div>

        <!-- pagination  -->
        <template v-if="projects">
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
