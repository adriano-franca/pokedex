<template>
    <div>
        <h1>{{ num }} {{ uppercase(name) }}</h1>
        <small>{{ url }}</small>
    </div>
</template>

<script>
export default {
    props: {
        num: Number,
        name: String,
        url: String
    },
    computed: {
        uppercase(value){
            console.log(value)
            var newName = value[0].toUpperCase() + value.slice(1);
            return newName;
        }
    }
}
</script>

<style>

</style>