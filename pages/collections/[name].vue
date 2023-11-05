<script setup lang="ts">
import { useCounterStore } from '~/plugins/pinia';

const route = useRoute()
const store = useCounterStore()

const question = ref('')
const answer = ref('')

const index = ref(1)
const id = ref(1)
const req = ref(1)

const { data: info } = await useAsyncData(() => {
    return $fetch(`https://drvcash.com/api/collections/${route.params.name}`)
}, {
    watch: [id]
})

let { data: posts }: any = await useAsyncData(() => {
    return $fetch(`https://drvcash.com/api/collections/${route.params.name}/getVectors`)
}, {
    watch: [id],
    // immediate: false
})

async function upsert() {

    await $fetch(`https://drvcash.com/api/collections/${route.params.name}/insert`, {
        method: 'POST',
        body: {
            question: question.value,
            answer: answer.value
        },
    }).then((status) => {
        console.log(status)
    }).catch(error => {
        console.log(error)
    })

        ; (function () {
            id.value++
            console.log(id.value)
        })();

    //  = $fetch(`http://localhost:5000/collections/${route.params.name}/getVectors`, {
    //     method: 'POST',
    //     body: {
    //         question: question.value,
    //         answer: answer.value
    //     },
    // })

}

async function deleteVector(vector: string) {
    console.log(vector)
    // const { data } = await useFetch(`http://localhost:5000/collections/firstParams/${uuid}`, {
    //     method: 'DELETE'
    // })}

    await $fetch(`https://drvcash.com/api/collections/${route.params.name}/${vector}`, {
        method: 'DELETE',
    }).then(() => {
        console.log('deleted')
    }).catch(error => {
        console.log(error)
    });

    (function () {
        id.value++
        console.log('id changed')
    })();
}
</script>

<template>
    <div class="container">
        <h3 class="mb-4">Collection: {{ route.params.name }}</h3>
        <div class="row my-5">
            <div class="col">
                <form class="mb-4" v-on:submit.prevent="">
                    <div class="mb-3">
                        <label for="question" class="form-label">Question</label>
                        <textarea class="form-control" id="question" placeholder="Awesome question"
                            v-model="question"></textarea>
                    </div>
                    <div class="mb-3">
                        <label for="exampleFormControlTextarea1" class="form-label">Answer</label>
                        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3"
                            placeholder="Some answer ..." v-model="answer"></textarea>
                    </div>
                    <button class="btn btn-primary" v-on:click="upsert()">Upsert</button>
                </form>
            </div>
            <div class="col">
                {{ info }}
                <!-- <p style="white-space: pre-line;">{{ info }}</p> -->
            </div>
        </div>
        <!-- <div class="method-list mt-4">
            <button class="btn btn-primary">Upsert Vectors</button>
            <button class="btn btn-primary">Edit Vectors</button>
        </div> -->
        <table class="table table-light table-striped table-hover table-bordered">
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
                <tr v-for="(prop, index) in posts[0]" :key="prop" :data-id="prop.meta">
                    <th scope="row">{{ index }}</th>
                    <td>{{ prop.meta }}</td>
                    <td>{{ prop.value }}</td>
                    <td><button class="btn btn-light"><i class="bi-eye"></i></button></td>
                    <td><button class="btn btn-success"><i class="bi-tools"></i></button></td>
                    <td><button v-on:click="deleteVector(prop.meta)" class="btn btn-danger"><i
                                class="bi-trash"></i></button></td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style lang="scss">
.method-list {
    display: flex;

    button {
        display: block;
        margin-right: .5rem;
    }
}
</style>