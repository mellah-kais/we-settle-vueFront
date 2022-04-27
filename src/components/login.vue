<template>
  <div class="container mt-5">
    <div class="row d-flex justify-content-center">
        <div class="col-md-6">
            <div class="card px-5 py-5" id="form1">
                <div class="form-data" >
                    <div class="forms-inputs mb-4"> <span>Email</span> <input autocomplete="off" type="text" v-model="email" v-bind:class="{'form-control':true, 'is-invalid' : !validEmail(email) && emailBlured}" @:blur="emailBlured = true">
                        <div class="invalid-feedback">A valid email is required!</div>
                    </div>
                    <div class="forms-inputs mb-4"> <span>Password</span> <input autocomplete="off" type="password" v-model="password" v-bind:class="{'form-control':true, 'is-invalid' : !validPassword(password) && passwordBlured}" @:blur="passwordBlured = true">
                        <div class="invalid-feedback">Password must be 8 character!</div>
                    </div>
                    <div class="mb-3"> <button v-on:click.stop.prevent="submit" class="btn btn-dark w-100">login</button> </div>

                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'userLogin',
  props: {
  },
  data() {
    return {
      email : "",
      password:"",
      emailBlured : false,
      valid : false,
      passwordBlured:false
    }
  },
  methods:{
    validate : function(){
      this.emailBlured = true;
      this.passwordBlured = true;
      if( this.validEmail(this.email) && this.validPassword(this.password)){
        this.valid = true;
      }
    },

    validEmail : function(email) {
      var re = /(.+)@(.+){2,}\.(.+){2,}/;
      if(re.test(email.toLowerCase())){
      return true;
      }
    },
    validPassword : function(password) {
      if (password.length > 7) {
      return true;
      }
    },
    submit :async function (){
      this.validate();
      if(this.valid){
        this.submitted = true;
        const {email,password} = this
        const user = await axios.post('http://localhost:3000/login',{email,password})
        this.$emit('getUserId',user.data)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body {
    background: #000
}

.card {
    border: none;
    height: 320px
}

.forms-inputs {
    position: relative
}

.forms-inputs span {
    position: absolute;
    top: -18px;
    left: 10px;
    background-color: #fff;
    padding: 5px 10px;
    font-size: 15px
}

.forms-inputs input {
    height: 50px;
    border: 2px solid #eee
}

.forms-inputs input:focus {
    box-shadow: none;
    outline: none;
    border: 2px solid #000
}

.btn {
    height: 50px
}

.success-data {
    display: flex;
    flex-direction: column
}

.bxs-badge-check {
    font-size: 90px
}
</style>
