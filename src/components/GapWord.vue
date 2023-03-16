<script setup>

</script>

<script>
export default {
    props: ["correctWord"],
    data() {
        return {
            color: "white",
            submission: "",
            length: this.correctWord.length
        }
    },
    methods: {
        update() {
            if (this.submission === this.correctWord) {

                this.color = "lime"

                if (this.points != 100) {
                    this.$emit('clicked', "Hello")
                }
                this.points = 100
            }
            else {
                this.color = "red"
            }
            console.log(this.submission)
            console.log(this.correctWord)
            console.log(this.color)
        }
    }
}
</script>

<template>
    <input v-model="submission" @keyup.enter="update" v-bind:size="length" />
</template>

<style scoped>
input {
    size: v-bind(length);
    color: v-bind(color);
    padding: 3px;
    border-radius: 5px;
    background: #242424;
    background:
        linear-gradient(white, white) center bottom 5px /calc(100% - 10px) 2px no-repeat;
}
</style>