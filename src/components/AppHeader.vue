<script>
export default {
    data() {
        return {
            navLinks: [
                {
                    label: 'Home',
                    routeName: 'home'
                },
                {
                    label: 'Projects',
                    routeName: 'projects'
                }
            ]
        }
    }
}
</script>

<template>
    <header>
        <nav class="navbar navbar-expand-lg bg-dark border-body" data-bs-theme="dark">
            <div class="container-fluid">
                <div class="navbar-brand">Boolfolio</div>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#main-nav"
                    aria-controls="main-nav" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse justify-content-end" id="main-nav">
                    <ul class="navbar-nav">
                        <li v-for="link in navLinks" class="nav-item">
                            <router-link :to="{ name: link.routeName }" activeClass="active" class="nav-link"
                                aria-current="page">{{ link.label }}</router-link>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>
</template>

<style lang="scss">
header {
    font-family: "Roboto Mono", monospace;
}
</style>