<template>
    <div>
        <h2 class="title">Form Validation</h2>
        <form @submit.prevent="submit" class="form">
            <label for="email" class="email">Email</label><br>
            <input type="email" placeholder="Email" v-model="state.email"><br>
            <p v-if="v$.email.$error">{{v$.email.$errors[0].$message}}</p>
            <label for="password" class="password">Password</label><br>
            <input type="password" placeholder="Password" v-model="state.password"><br>
            <p v-if="v$.password.$error">{{v$.password.$errors[0].$message}}</p>
            <label for="confirmPassword" class="confirmPassword">ConfirmPassword</label><br>
            <input type="password" placeholder="Confirm Password" v-model="state.confirmPassword"><br>
            <p v-if="v$.confirmPassword.$error">{{v$.confirmPassword.$errors[0].$message}}</p>
            <input type="submit" value="Submit" class="submit">
        </form>
    </div>
</template>
<script>
import useValidate from "@vuelidate/core";
import {required,email,sameAs,minLength,helpers} from "@vuelidate/validators";
import {reactive,computed} from "vue";
export default {
    name:"Form",
    setup() {
        const state = reactive({
            email:"",
            password:"",
            confirmPassword:"",
        })
        const rules = computed(() => {
            return {
            email:{ required: helpers.withMessage('This field cannot be empty', required), email},
            password:{required: helpers.withMessage('This field cannot be empty', required), minLength:minLength(6)},
            confirmPassword:{required, sameAs: sameAs(state.password)},
            }
        })
        const v$ = useValidate(rules,state);
        return {
            state,
            v$
        }
    },
    methods: {
        submit() {
            this.v$.$validate();
            if(!this.v$.$error) {
                alert("Form successfully submitted!!")
            }
        }
    }
}
</script>
<style scoped>
.title {
    text-align:center;
}
.form {
    width:29rem;
    max-height:25rem;
    background:#eee;
    border-radius:0.5rem;
    padding:1.5rem;
    margin-top:1rem;

}
input {
    padding:10px 3px;
    width:400px;
    border:none;
    outline:none;
    border-bottom:1px solid #000;
    border-radius:3px;
    margin:10px 0 10px 0;
    background-color:#eee;
}
input:focus {
    background-color:#eee;
}
p {
    margin:0.1rem 0 0.3rem 0;
    color:#ff0000;
}
.submit {
    background:#06a706;
    color:#fff;
    font-size:1rem;
    border-radius:3px;
    border:none;
    outline:none;
    margin-top:1rem;
}
.submit:focus {
    background:#06a706;
    color:#fff;
    font-size:1rem;
    border-radius:3px;
    border:none;
    outline:none;
    margin-top:1rem;
}
.submit:hover {
    background:#099b09;
}
</style>