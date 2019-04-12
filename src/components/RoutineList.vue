<template>
    <b-row>
        <b-col cols="12">
        
		<b-link href="sign-in">Sign-In</b-link>&nbsp;&nbsp;
		<b-link href="sign-in">Exercise Library</b-link>
		
		<br><br>
		
		<b-jumbotron>
            <b-form @submit="onSubmit">
            <b-form-group id="fieldsetHorizontal"
                        horizontal
                        :label-cols="4"
                        breakpoint="md"
                        label="Please enter the name of your new routine">
                <!-- 
				<b-form-input id="routine_name" v-model.trim="routine.routine_name"></b-form-input>
				-->
            </b-form-group>
            <b-button type="submit" variant="primary">Save</b-button>
            </b-form>
        </b-jumbotron>
	  
	    </b-col>


	

		<h2>
                My Routines
                <b-link href="#/add-routine">(New Routine)</b-link>
            </h2>
            <b-table striped hover :items="routines" :fields="fields">
                <template slot="actions" scope="row">
                    <b-btn size="sm" @click.stop="details(row.item)">Details</b-btn>
                </template>
            </b-table>
        </b-col>
    </b-row>
	
</template>

<script>

    import firebase from '../Firebase'
    import router from '../router'

    export default {
        name: 'Addroutine',
        data () {
            return {
            ref: firebase.firestore().collection('routines'),
            routine: {}
            }
        },

        name: 'RoutineList',
        data () {
            return {
                fields: {
                    routine_name: { label: 'routine_name', sortable: true, 'class': 'text-left' },
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
                        routine_name: doc.data().routine_name
                    });
                });
            });
        },
        methods: {
            details (routine) {
                router.push({ name: 'Showroutine', params: { id: routine.key }})
            },

            onSubmit (evt) {
                evt.preventDefault()

                this.ref.add(this.routine).then((docRef) => {
                    this.routine.routine_name = ''
                    router.push({
                    name: 'Addroutine'
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