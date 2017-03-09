<template>
    <div class="styleEditor" ref="container">
        <div class="styleCode" v-html="styleCode"></div>
        <pre v-html="highlightedCode"></pre>
    </div>
</template>
<script>
import Prism from 'prismjs'
export default {
    name: 'styleEditor',
    props: ['code'],
    computed: {
        styleCode: function() {
            return `<style>${this.code}</style>`
        },
        highlightedCode: function() {
            return Prism.highlight(this.code, Prism.languages.css)
        }
    },
    methods: {
        goBottom: function() {
            this.$refs.container.scrollTop = 10000
        }
    }

}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.styleCode {
    display: none;
}
</style>
