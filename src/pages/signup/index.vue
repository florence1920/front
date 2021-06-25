<template>
    <div class="mt-4 "> 
         <b-form @submit.prevent="onSubmit">
            <ValidationProvider
                name="Name"
                rules="required"
                v-slot="{errors}"
            >
                <b-form-group label="Name:">
                    <b-form-input
                        v-model="form.name"
                        type="text"
                        required
                    ></b-form-input>
                    <FormErrorMessage :errors="errors" />
                </b-form-group>
            </ValidationProvider>

            <ValidationProvider
                name="Email"
                rules="required|email"
                v-slot="{errors}"
            >
                <b-form-group label="Email address:">
                    <b-form-input
                        v-model="form.email"
                        type="email"
                        required
                    ></b-form-input>
                <FormErrorMessage :errors="errors" />
                </b-form-group>
            </ValidationProvider>
            

            <ValidationProvider
                name="Password"
                rules="required|min:6"
                v-slot="{errors}"
            >
                <b-form-group label="Password:">
                    <b-form-input
                        v-model="form.password"
                        type="password"
                        required
                    ></b-form-input>
                <FormErrorMessage :errors="errors" />
                </b-form-group>
            </ValidationProvider>


            <ValidationProvider
                name="PasswordConfirm"
                rules="required|min:6"
                v-slot="{errors}"
            >
            <b-form-group label="Confirm Password:">
                <b-form-input
                    v-model="form.passwordConfirm"
                    type="password"
                    required
                ></b-form-input>
                <FormErrorMessage :errors="errors" />
            </b-form-group>
            </ValidationProvider>

            <b-button type="submit" variant="primary">SignUp</b-button>
        </b-form>
    </div>
</template>

<script>
import axios from 'axios';
import {ValidationProvider} from 'vee-validate';
import FormErrorMessage from '@/components/FormErrorMessage.vue'
export default {
    components:{
        ValidationProvider,
        FormErrorMessage
    },
    data() {
        return{
            form:{
                name:'',
                email:'',
                password:'',
                passwordConfirm:''
            }
        }
    },
    methods:{
        async onSubmit(){
            try{
                await axios.post('http://localhost:3000/auth/signup',{
                    email:this.form.email,
                    password:this.form.password,
                    name: this.form.name
                })
                this.$router.push({path:'/login'})
            }catch(err){
                console.log(err);
            }
        }
    }
}
</script>