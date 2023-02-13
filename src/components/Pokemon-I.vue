<template>
    <div>
        <h1>{{ num }} {{ name.toUpperCase() }}</h1>
        <small>{{ url }}</small>
    </div>
</template>

<script>

import axios from 'axios'
export default {
    props: {
        num: Number,
        name: String,
        url: String
    },
}
</script>

<style>

</style>