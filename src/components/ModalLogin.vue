<template>
  <modal
    title="Login"
    @close="close">
    <!-- body -->
    <div slot="body">
      <form @submit.prevent="onSubmit">

        <!-- email -->
        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required"> Filed is required! </p>
          <p class="errorText" v-if="!$v.email.email"> Email is not correct!</p>
          <input
            v-model="email"
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()">
        </div>

				<!-- password -->
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password:</label>
          <p class="errorText" v-if="!$v.password.required"> Password is required! </p>
					<p class="errorText" v-if="!$v.password.minLength">Password must have at least {{ $v.password.$params.minLength.min }} letters.</p>
          <input
            v-model="password"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()">

        </div>
        <!-- button -->
        <button class="btn btnPrimary">Login!</button>
				<div>Need registration? <span @click="$emit('swap-form')">Enter Here</span></div>
      </form>
    </div>
  </modal>
</template>

<script>
import { required, minLength, email } from 'vuelidate/lib/validators'

import modal from '@/components/UI/Modal.vue'

export default {
  components: { modal },
  data () {
    return {
			email: '',
			password: ''
    }
  },
  validations: {
    email: {
      required,
      email
		},
		password: {
			required,
			minLength: minLength(6)
		}
	},
	methods: {
		onSubmit () {
			this.$v.$touch()
			if (!this.$v.$invalid) {
				const user = {
					name: this.name,
					email: this.email
				}
				console.log(user)

				//DONE!
				this.email = ''
				this.password
				this.$v.$reset()
				this.$emit('close')
			}
		},
		 close () {
      this.$emit('close');
			this.email = '';
			this.password = '';
			this.$v.$reset()
    },
	}
}
</script>

<style lang="scss">
.form-item .errorText {
	display: none;
	margin-bottom: 8px;
	font-size: 13.4px;
	color: #de4040;
}
.form-item {
	&.errorInput .errorText {
		display: block;
	}
}
input.error {
	border-color: #de4040;
}
</style>
