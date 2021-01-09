<template>
    <main>
        <p v-if="$fetchState.pending">Fetching the notes...</p>
        <p v-else-if="$fetchState.error">Could not find any notes</p>
        <div v-else>
            <h1>{{ notes.title | capitalize }} Note</h1>
            <p><br>{{notes.note}}</p>
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

<style scoped>
    main {
        display: grid;
        text-align: center;
        align-items: center;
    }
    
    div {
        padding: 5%;
        padding-bottom: 20%;
        padding-top: 1%;
    }
</style>

<style>
    html,body,#__layout {
        display: grid;
        padding: 0;
        margin: 0;
        height: 100%;
        width: 100%;
        overflow: hidden;
    }

    body {
        background-color: lightpink;
    }
    
    h1,p {
        font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    }

    h1 {
        color: white;
    }

    p {
        color: darkslategray;
    }
</style>