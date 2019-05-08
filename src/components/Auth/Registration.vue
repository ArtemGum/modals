<template>
  <modal
    title="Registration"
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
						type="password"
            v-model="password"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch()">

				<!-- Repeat Password -->
        <div class="form-item" :class="{ errorInput: $v.repeatPassword.$error }">
          <label>Repeat password:</label>
          <p class="errorText" v-if="!$v.repeatPassword.sameAsPassword">Passwords must be identical.</p>
          <input
						type="password"
            v-model="repeatPassword"
            :class="{ error: $v.repeatPassword.$error }"
            @change="$v.repeatPassword.$touch()">
        </div>

        </div>
        <!-- button -->
        <button class="btn btnPrimary">Registration!</button>
				<div>Do you have account? <a style="cursor: pointer; color: #444ce0;" @click="$emit('login')">Enter Here</a></div>
      </form>
    </div>
  </modal>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'

import modal from '@/components/UI/Modal.vue'

export default {
  components: { modal },
  data () {
    return {
			email: '',
			password: '',
			repeatPassword: ''
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
		},
		repeatPassword: {
			sameAsPassword: sameAs('password')
		}
	},
	methods: {
		onSubmit () {
			this.$v.$touch()
			if (!this.$v.$invalid) {
				const user = {
					email: this.email,
					password: this.password
				}
				console.log(user)

				//DONE!
				this.email = ''
				this.password = ''
				this.$v.$reset()
				this.$emit('close')
			}
		},
		 close () {
      this.$emit('close');
			this.email = '';
			this.password = '';
			this.repeatPassword = '';
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
