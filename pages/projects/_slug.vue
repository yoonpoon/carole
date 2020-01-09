<template>
  <section>
    <h1> {{project.title}} </h1>
  </section>
</template>

<script>
import gql from 'graphql-tag'

export default {
  data() {
    return {
      project: {},
      loading: 0
    }
  },
  apollo: {
    project: {
      query: gql`query Project($slug: String!) {
        project(filter: {slug: {matches: {pattern: $slug }}}) {
          title
          slug
        }
      }`,
      variables() {
        return {
          slug: this.$route.params.slug
        }
      },
      prefetch: ({ route }) => ({ slug: route.params.slug })
    }
  }
}
</script>
