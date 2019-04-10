<template>
    <b-row>
        <b-col cols="12">
        <b-jumbotron>
            <b-form @submit="onSubmit">
            <b-form-group id="fieldsetHorizontal"
                        horizontal
                        :label-cols="4"
                        breakpoint="md"
                        label="Enter Title">
                <b-form-input id="title" v-model.trim="board.title"></b-form-input>
            </b-form-group>
            <b-form-group id="fieldsetHorizontal"
                        horizontal
                        :label-cols="4"
                        breakpoint="md"
                        label="Enter Description">
                <b-form-textarea id="description"
                            v-model="board.description"
                            placeholder="Enter something"
                            :rows="2"
                            :max-rows="6">{{board.description}}</b-form-textarea>
            </b-form-group>
            <b-form-group id="fieldsetHorizontal"
                        horizontal
                        :label-cols="4"
                        breakpoint="md"
                        label="Enter Author">
                <b-form-input id="author" v-model.trim="board.author"></b-form-input>
            </b-form-group>
            <b-button type="submit" variant="primary">Save</b-button>
            </b-form>
        </b-jumbotron>
	  
	    </b-col>
  </b-row>
	

</template>

<script>

    import firebase from '../Firebase'
    import router from '../router'

    export default {
        name: 'AddBoard',
        data () {
            return {
            ref: firebase.firestore().collection('routines'),
            board: {}
            }
        },

        name: 'RoutineList',
        data () {
            return {
                fields: {
                    title: { label: 'Title', sortable: true, 'class': 'text-left' },
                    actions: { label: 'Action', 'class': 'text-center' }
                },
                routines: [],
                errors: [],
                ref: firebase.firestore().collection('routines'),
            }
        },
        
        created () {
            this.ref.onSnapshot((querySnapshot) => {
                this.routines = [];
                querySnapshot.forEach((doc) => {
                    this.routines.push({
                        key: doc.id,
                        title: doc.data().routine_name
                    });
                });
            });
        },
        methods: {
            details (routine) {
                router.push({ name: 'Showroutine', params: { id: routine.key }})
            }

            onSubmit (evt) {
                evt.preventDefault()

                this.ref.add(this.routine).then((docRef) => {
                    this.routine.title = ''
                    this.routine.description = ''
                    this.routine.author = ''
                    router.push({
                    name: 'AddBoard'
                    })
                })
                .catch((error) => {
                    alert("Error adding document: ", error);
                });
            }
        }
    }
</script>

<style>
    .table {
        width: 96%;
        margin: 0 auto;
    }
    .jumbotron {
        padding: 2rem;
    }
    .edit-btn {
        margin-right: 20px;
        width: 70px;
    }
</style>