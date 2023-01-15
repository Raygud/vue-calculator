<template>
    <div>

        {{ Solved? null: Sum }}


        {{ Solved? Solved: null }}


        {{ Method }}

        {{ NumberToProcess? NumberToProcess: null }}

    </div>
</template>

<script>
export default {
    props: {
        Sum: {
            type: Number,
            required: true
        },
        NumberToProcess: {
            type: Number,
            required: true
        },
        Solved: {
            type: Number,
            required: true
        },
        Method: {
            type: String,
            required: true
        }
    },
    setup() {


        return {}
    }
}
</script>

<style scoped>
@font-face {
    font-family: PixelFont;
    src: url('~@/assets/fonts/Minecraft.ttf');
}

div {
    box-sizing: border-box;
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: flex-end;
    width: 100%;
    height: 25vh;
    background-color: rgb(34, 36, 34);
    color: rgb(255, 255, 255);
    font-size: 15vw;
    padding: 5vw;
    margin-bottom: 15vw;
    font-family: PixelFont;
    /* animation: RetroBlink 2s infinite; */
}

/* @keyframes RetroBlink {
    0% {
        color: rgb(255, 255, 255);
    }

    99% {
        color: rgb(255, 255, 255);
    }

    100% {
        color: rgba(0, 255, 255, 0);

    }
} */
</style>