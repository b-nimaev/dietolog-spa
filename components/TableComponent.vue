<script setup lang="ts">
const props = defineProps(['params'])
const id = ref('')
const route = useRoute()
const { data: info } = await useAsyncData(() => {
    return $fetch(`https://drvcash.com/api/collections/${route.params.name}/${id}`, {
        method: 'DELETE'
    })
}, {
    watch: [id]
})
// const updateDelete = async (uuid: string) => {
    // Because your composable is called in the right place in the lifecycle,
    // useRuntimeConfig will also work
    // const config = useRuntimeConfig()

    // console.log(uuid)
    // const { data } = await useFetch(`https://drvcash.com/api/collections/firstParams/${uuid}`, {
    //     method: 'DELETE'
    // })
    // console.log(id.value)
    // console.log(data.value)

    // ...
// }
</script>

<template>
    <table class="table table-dark table-striped table-hover table-bordered">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">uuid</th>
                <th scope="col">value</th>
                <th scope="col">2par</th>
                <th scope="col">edit</th>
                <th scope="col">delete</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(prop, index) in props.params[0]" :key="prop" :data-id="prop.meta">
                <th scope="row">{{ index }}</th>
                <td>{{ prop.meta }}</td>
                <td>{{ prop.value }}</td>
                <td><button class="btn btn-light"><i class="bi-eye"></i></button></td>
                <td><button class="btn btn-success"><i class="bi-tools"></i></button></td>
                <td><button @click="id=prop.meta" class="btn btn-danger"><i class="bi-trash"></i></button></td>
            </tr>
        </tbody>
    </table>
</template>pr