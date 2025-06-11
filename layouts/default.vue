<template>
    <v-app>
        <headerLayout/>
            <v-slot>
                <nuxt-page />
            </v-slot>
        <footerLayout/>
    </v-app>
</template>

<script setup>
    import headerLayout from '/components/headerLayout.vue'
    import footerLayout from '/components/footerLayout.vue'
</script>