<script>
import axios from 'axios';

export default {
    name: 'SingleProject',
    props: {
        projectDetails: Object
    },
    methods: {
        truncate(text) {
            if (text.length > 100) {
                return text.substr(0, 99) + '[...]';
            }
            return text;
        }
    }
}
</script>

<template>

    <div class="col my-3">
        <div class="card h-100">
            <div class="card-body">
                <h5 class="card-title fw-bold">{{ projectDetails.name }}</h5>

                <div><span class="fw-bold">Client: </span>{{ projectDetails.client_name }}</div>

                <div v-if="projectDetails.type"><span class="fw-bold">Type: </span>{{ projectDetails.type.name }}</div>

                <template v-if="projectDetails.technologies.length > 0">
                    <div class="fw-bold mb-1">Technologies:</div>
                    <div class="d-flex flex-wrap gap-1">
                        <div v-for="technology in projectDetails.technologies" class="badge text-bg-secondary">
                            {{ technology.name }}
                        </div>

                    </div>
                </template>

                <p class="mt-2">{{ truncate(projectDetails.summary) }}</p>

            </div>
        </div>
    </div>

</template>
