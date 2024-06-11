<script>
export default {

}
</script>

<template>
    <header>
        <nav class="navbar navbar-expand-lg bg-dark border-bottom border-body" data-bs-theme="dark">
            <div class="container-fluid">
                <a class="navbar-brand">Boolfolio</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
                    aria-controls="main-nav" aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="collapse navbar-collapse" id="main-nav">
                    <ul class="navbar-nav">
                        <li class="nav-item">
                            <router-link :to="{ name: 'home' }" activeClass="active" class="nav-link"
                                aria-current="page">Home</router-link>
                        </li>
                        <li class="nav-item">
                            <router-link :to="{ name: 'projects' }" activeClass="active"
                                class="nav-link">Projects</router-link>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>
</template>