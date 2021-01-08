<template>
    <main>
        <h1>Random Note</h1>
        <p v-if="$fetchState.pending">Fetching the notes...</p>
        <p v-else-if="$fetchState.error">Could not find any notes</p>
        <div v-else>
            <p><b>{{notes.title | capitalize}}</b><br>{{notes.note}}</p>
        </div>
        </main>
</template>

<script>
export default {
    data() {
        return {
            notes: []
        }
    },
    async fetch() {
        this.notes = await fetch(
            'http://localhost:3000/notes.json'
        ).then(res => res.json()).then(function (data){
            var choice = Math.floor(Math.random() * data.length);
            console.log(choice);
            console.log(data[choice]);
            return data[choice];
        })
    },
    filters: {
        capitalize: function(value) {
            if (!value) return ''
            value = value.toString()
            return value.charAt(0).toUpperCase() + value.slice(1)
        }
    }
}
</script>