<template>
    <div id='addTodo' v-if='getLoggedInStatus'>
        <div id='addForm'>
            <h2 class='header'>CREATE YOUR TODO</h2>

            <p v-if='submitted'>Your todo has been created! You can check it out <router-link to='/todos' exact>here</router-link></p>
            
            <form v-if='!submitted' v-on:submit.prevent='postTodo'>
                <ul>
                    <li>
                        <label for='titleInput'>Title: </label>
                        <input id='titleInput' type='text' v-model='todo.title' placeholder="Todo's Title" required/>
                    </li>
                    <li>
                        <label for='descriptionInput'>Description: </label>
                        <textarea id='descriptionInput' v-model='todo.description' placeholder="Todo's Description" required></textarea>
                    </li>
                </ul>

                <button>CREATE!</button>
            </form>
        </div>
    </div>
</template>

<script>
import { db } from '../../config/firebaseConfig';
import { mapGetters } from 'vuex';
import firebase from 'firebase';

export default {
    data() {
        return {
            todo: {
                title: '',
                description: '',
                date: ''
            },
            submitted: false
        };
    },
    methods: {
        postTodo() {
            this.date = new Date();

            db.collection('todos').add({
                title: this.todo.title,
                description: this.todo.description,
                author: this.getUserEmailName,
                date: firebase.firestore.FieldValue.serverTimestamp()
            });
            this.submitted = true;
        }
    },
    computed: {
        ...mapGetters([
            'getUserEmailName',
            'getLoggedInStatus'
        ])
    }
}
</script>

<style scoped lang='scss'>

a {
    color: #444;
}

#addTodo {
    margin-top: 100px;
    display: flex;
    justify-content: center;
}
#addForm {
    width: 800px;
    background: #fff;
    padding: 20px;

    form {
        text-align: center;
        width: 50%;
        margin: 0 auto;
    }
    textarea {
        margin: 10px 0;
        min-height: 50px;
        font-family: Roboto, Arial, Helvetica, sans-serif;
        resize: none;
        border: 1px solid #ddd;
        width: 100%;
        font-size: 15px;
        height: 200px;
    }
    input:focus, textarea:focus {
        outline: none;

        -webkit-box-shadow: inset 0 0 1px #000;
        box-shadow: inset 0 0 1px #000;
    }
    label {
        text-align: left;
        display: block;
        font-size: 18px;
        margin: 0 0 10px 0;
    }
    input, textarea {
        width: 100%;
        display: block;
        padding: 10px;
        -moz-border-radius: 5px;
        -webkit-border-radius: 5px;
        border-radius: 5px;

        -moz-transition: box-shadow 0.1s;
        -webkit-transition: -webkit-box-shadow 0.1s;
        -o-transition: box-shadow 0.1s;
        transition: box-shadow 0.1s;
    }
    input[type=text] {
        border: 0;
        border: 1px solid #ddd;
        font-size: 15px;
    }
    button {
        background: #666;
        border: 0;
        color: #fff;
        padding: 10px;
        font-family: Roboto, Arial, Helvetica, sans-serif;
        cursor: pointer;
        font-size: 16px;
        width: 130px;

        &:hover {
            background: #444;
        }
    }
}

ul {
    padding: 0;
    width: 100%;
    list-style-type: none;
    li {
        margin: 20px 0;
    }
}

.header {
    text-align: center;
    font-size: 28px;
}

p {
    text-align: center;
}

@media screen and (max-width: 950px) {

    h2.header {
        font-size: 28px;
    }

    #addForm {

        width: 80%;

        form {
            width: 400px;
        }

        button {
            font-size: 16px;
        }

        label {
            font-size: 16px;
        }
    }
}

@media screen and (max-width: 586px) {
    #addForm {
        width: 100%;
        form {
            width: 100%;
        }

        h2.header {
            font-size: 24px;
        }

        label {
            font-size: 14px;
        }

        button {
            font-size: 14px;
        }
    }
}
</style>