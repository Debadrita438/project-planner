<template>
    <form @submit.prevent='handleSubmit'>
        <label>Title:</label>
        <input v-model='title' type="text" required>

        <label>Details:</label>
        <textarea v-model='details' required></textarea>

        <button>Add Project</button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                title: '',
                details: ''
            }
        },
        methods: {
            handleSubmit() {
                let project = {
                    title: this.title,
                    details: this.details,
                    complete: false
                }
                fetch('http://localhost:3000/projects', {
                    method: 'POST',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(project)
                })
                    .then(() => this.$router.push('/'))
                    .catch(err => console.log(err.message))
            }
        }
    }
</script>

<style>
    form{
        background:#21252b;
        padding: 20px;
        border-radius: 10px;
    }

    label {
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        letter-spacing: 1px;
        margin: 20px 0 10px 0;
    }

    input {
        padding: 10px;
        border: 0;
        box-sizing: border-box;
        border-radius: 4px;
        border-style: groove;
        border-width: 2px;
        border-color: #767676;
        width: 100%;
    }

    textarea {
        padding: 10px;
        border: 0;
        box-sizing: border-box;
        border-radius: 4px;
        border-style: groove;
        border-width: 2px;
        border-color: #767676;
        height: 100%;
        width: 100%;
    }

    form button {
        display: block;
        margin: 20px auto 0;
        background: #0d1117;
        color: #c9d1d9;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
        cursor: pointer;
        text-transform: uppercase;
        font-size: 0.8em;
        font-weight: bold;
    }
</style>