<script>
export default {}
</script>

<template>
    <div id='universe'>
        <div id='galaxy'>
            <div class='circle'></div>
            <div class='circle2'></div>
            <div class='circle3'></div>
            <div id='orbit0'>
                <div id='pos0'>
                    <div id='dot0'></div>
                </div>
            </div>
            <div id='orbit1'>
                <div id='pos1'>
                    <div id='dot1'></div>
                </div>
            </div>
            <div id='orbit2'>
                <div id='pos2'>
                    <div id='dot2'></div>
                </div>
            </div>
            <div id='orbit3'>
                <div id='pos3'>
                    <div id='dot3'></div>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
#universe {
    z-index: 1;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 100%;
    height: 100%;
}

#galaxy {
    transform: rotateX(75deg);
    transform-style: preserve-3d;
    position: relative;
    width: 100%;
    height: 100%;
}

.circle {
    border-radius: 50%;
    border: 1px solid #000;
    width: 1em;
    height: 1em;
    margin-top: -.5em;
    margin-left: -.5em;
    animation: spinner 1.5s infinite ease;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: rotateX(-75deg);
}

.circle2 {
    border-radius: 50%;
    border: 1px solid #000;
    width: 1em;
    height: 1em;
    margin-top: -.5em;
    margin-left: -.5em;
    animation: spinner2 2s infinite ease;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: rotateX(-75deg);
}

.circle3 {
    border-radius: 50%;
    border: 1px solid #000;
    width: 1em;
    height: 1em;
    margin-top: -.5em;
    margin-left: -.5em;
    animation: spinner3 2.5s infinite ease;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: rotateX(-75deg);
}


.orbit {
    transform-style: preserve-3d;
    position: absolute;
    top: 50%;
    left: 50%;
    animation-name: orbit;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
    width: 8em;
    height: 8em;
    margin-top: -4em;
    margin-left: -4em;
    border-radius: 50%;
}

.pos {
    position: absolute;
    width: 2em;
    height: 2em;
    margin-left: -1em;
    margin-top: -1em;
    animation-name: invert;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
    left: 50%;
    top: -1px;
}

.dot {
    background-color: #000;
    width: .5em;
    height: .5em;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -.25em;
    margin-left: -.25em;
    border-radius: 50%;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
}

$i: 0;

@while $i < 3 {
    #orbit#{$i} {
        @extend .orbit;
        animation-delay: -$i + s;
    }

    #pos#{$i} {
        @extend .pos;
        animation-delay: -$i + s;
    }

    #dot#{$i} {
        @extend .dot;
        animation-delay: -$i + s;
    }

    $i: $i + 1;
}

/* Planet animation durations */
.orbit,
.pos {
    animation-duration: 3s;
}

.circle {
    font-size: 6em;
}

.circle2 {
    font-size: 5em;
}

.circle3 {
    font-size: 4em;
}

.dot {
    font-size: 0.2em;
}

@keyframes orbit {
    0% {
        transform: rotateZ(0deg);
    }

    100% {
        transform: rotateZ(-360deg);
    }
}

@keyframes invert {
    0% {
        transform: rotateX(-90deg) rotateY(360deg) rotateZ(0deg);
    }

    100% {
        transform: rotateX(-90deg) rotateY(0deg) rotateZ(0deg);
    }
}

@keyframes spinner {
    0% {
        transform: rotate3d(1, 0, 1, 0deg);
    }

    50% {
        transform: rotate3d(1, 0, 1, 180deg);
    }

    100% {
        transform: rotate3d(1, 0, 1, 360deg);
    }
}

@keyframes spinner2 {
    0% {
        transform: rotate3d(0, 1, 1, 0deg);
    }

    50% {
        transform: rotate3d(0, 1, 1, 180deg);
    }

    100% {
        transform: rotate3d(0, 1, 1, 360deg);
    }
}

@keyframes spinner3 {
    0% {
        transform: rotate3d(1, 1, 0, 0deg);
    }

    50% {
        transform: rotate3d(1, 1, 0, 180deg);
    }

    100% {
        transform: rotate3d(1, 1, 0, 360deg);
    }
}
</style>
