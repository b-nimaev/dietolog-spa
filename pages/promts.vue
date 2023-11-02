<script setup lang="ts">

const id = ref(1)

const question = ref('')
const answer = ref('')

const { data: promts }: any = await useAsyncData(() => {
    return $fetch(`http://localhost:5000/promts`)
}, {
    watch: [id],
    // immediate: false
})
async function deletePromt(id: string) {
    try {

    } catch (error) {
        console.log(error)
    }
}
async function quest() {
    try {
        return $fetch(`http://localhost:5000/promts/test`, {
            method: 'POST',
            body: {
                question: question.value
            }
        }).then((response: any) => {
            console.log(response)
            if (typeof(response.choices[0].message.content) === 'string') {
                answer.value = response.choices[0].message.content
            }
        })
    } catch (error) {
        console.log(error)
    }
}
</script>

<template>
    <h2>Промты</h2>
    <div class="my-5">
        <h3>testing chat</h3>
        <div class="row my-4">
            <div class="col">
                <h5>user</h5>
                <form class="mb-4" v-on:submit.prevent="">
                    <div class="mb-3">
                        <label for="question" class="form-label">Question</label>
                        <textarea class="form-control" style="min-height: 200px; border-radius: 5px;" id="question" placeholder="Awesome question"
                            v-model="question"></textarea>
                    </div>
                    <button class="btn btn-primary" v-on:click="quest()">Send</button>
                </form>
            </div>
            <div class="col">
                <h5>bot</h5>
                <p style="margin-bottom: .5rem">answer</p>
                <div style="border: 1px solid #ececec; min-height: 200px; border-radius: 5px;">
                    {{ answer ? answer : '' }}
                </div>
            </div>
        </div>
    </div>
    <table class="table table-light table-striped table-hover table-bordered">
        <thead>
            <tr>
                <th scope="col">#</th>
                <th scope="col">_id</th>
                <th scope="col">content</th>
                <th scope="col">edit</th>
                <th scope="col">delete</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="(prop, index) in promts" :key="prop" :data-id="prop._id">
                <th scope="row">{{ index }}</th>
                <td>{{ prop._id }}</td>
                <td>{{ prop.content }}</td>
                <td><button class="btn btn-success"><i class="bi-tools"></i></button></td>
                <td><button v-on:click="deletePromt(prop._id)" class="btn btn-danger"><i class="bi-trash"></i></button>
                </td>
            </tr>
        </tbody>
    </table>
</template>