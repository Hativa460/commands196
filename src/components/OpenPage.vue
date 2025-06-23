<template>
    <div id="open-page">
        <div id="title">פקודות צוות מרכבה</div>
        <div id="button" @click="nextPage">מתחילים</div>
        <img id="prtankBtn" src="@/assets/media/prbarTank.png" alt="prtank">
    </div>
</template>

<script>
export default {
    name: "open-page",
    props: [],
    data() {
        return {

        }
    },
    methods: {
        nextPage() {
            this.$emit('next-page');
        }
    }
}
</script>

<style scoped>
#title{
    font-family: "asakim";
    font-size: 5rem;
    margin: auto;
    text-align: center;
    margin-top: 70%;
    color: #f6f7e8;
    text-shadow: 10px -2px 10px rgba(0, 0, 0, 0.5);
}

#button {
        margin: auto;
        margin-top: 7%;
        margin-bottom: 2%;
        font-family: "asakim";
        color: #f6f7e8;
        text-shadow: 5px -2px 5px rgba(0, 0, 0, 0.5);
        background-color: #7FCD91;
        border-radius: 1.5vh;
        padding: 3%;
        width: 35vw;
        font-size: 9vw;
        text-align: center;
        font-weight: 570;
        box-shadow: rgba(34, 34, 38, 0.2) 0px 7vw 29vw 0px;
        animation: scaling 1.1s linear infinite alternate;
        -webkit-animation: scaling 1.1s linear infinite alternate;
    }

    #prtankBtn {
        margin: auto;
        margin-top: -10%;
        margin-right: 15%;
        width: 25%;
        height: 25%;
        cursor: pointer;
        z-index: 1;
        animation: scaling 1.1s linear infinite alternate;
        -webkit-animation: scaling 1.1s linear infinite alternate;
    }

    @keyframes scaling {
        from {
            scale: 1;
        }
        to {
            scale: 1.05;
        }
    }
    @-webkit-keyframes scaling {
        from {
            scale: 1;
        }
        to {
            scale: 1.05;
        }
    }
</style>