<template>

</template>

<script>
export default {
    data() {
        return {
            requestBody: this.$route.query,
            idx: this.$route.query.idx,
            title: '',
            author: '',
            contents: '',
            created_at: '',
        }
    },
    mounted() {
        this.fnGetView()
    },
    methods: {
        fnGetView() {
            if (this.idx !== undefined) {
                
            }
        }
    }
}
</script>