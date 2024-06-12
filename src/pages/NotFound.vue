<script>
</script>

<template>
    <div class="lost-bg vstack justify-content-center align-items-center text-white">
        <div class="text-center z-3">
            <h1 class="fw-bold">Ops! Looks like you're lost!</h1>
            <div class="text-uppercase">page not found.</div>
        </div>
        <div class="ms-img-container vstack justify-content-center align-items-center">
            <div class="hstack justify-content-center align-items-center">
                <img id="space-cat" src="/src/assets/img/space-cat-nobg.png" alt="space-cat">
                <router-link :to="{ name: 'home' }" id="go-home"
                    class="text-uppercase text-white text-decoration-none border rounded-5 p-2">Go
                    home</router-link>
            </div>
            <img class="" id="yarn-ball" src="/src/assets/img/yarn-ball-block.png" alt="yarn-ball">
        </div>
    </div>
</template>

<style lang="scss">
.lost-bg {
    height: calc(100vh - 57px);
    background-image: url('src/assets/img/lost-in-space.jpeg');
    background-repeat: no-repeat;
    background-size: cover;
    font-family: "Roboto Mono", monospace;
    overflow: hidden;

    .ms-img-container {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        width: 700px;
        height: 600px;

        #space-cat {
            width: 30%;
            z-index: 10;
            position: relative;
            animation: spaceMove 5s ease-in-out infinite;
        }

        #go-home:hover {
            box-shadow: 5px 5px 5px #fff;
        }

        #yarn-ball {
            width: 100%;
        }
    }
}

@keyframes spaceMove {
    0% {
        left: 0px;
        top: 0px;
    }

    25% {
        left: 0px;
        top: 5px;
    }

    50% {
        left: 0px;
        top: 10px;
    }

    75% {
        left: 0px;
        top: 5px;
    }

    100% {
        left: 0px;
        top: 0px;
    }
}

@media screen and (max-width: 710px) {
    .lost-bg {
        .ms-img-container {
            #yarn-ball {
                width: 70%;
            }
        }
    }

}
</style>