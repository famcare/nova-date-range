<template>
    <panel-item :field="field" />
</template>

<script>
export default {
    props: {
        resource: String,
        resourceName: String,
        resourceId: [String, Number],
        field: Object,
    },
}
</script>
