<template>
<div class="wrapper">
	<div class="wrapper-content">

		<section>
			<div class="container">

				 <!-- registration modal -->
				<button class="btn btnPrimary" @click="auth = 'register'">Registration</button>
				<modalRegistration @login="auth = 'login'" v-show="auth === 'register'" @close="auth = null"/>

				<!-- Login modal -->
				<button class="btn btnPrimary" @click="auth = 'login'">Login</button>
				<modalLogin @register="auth = 'register'" v-show="auth === 'login'" @close="auth = null" />

			</div>
		</section>
	</div>

</div>

</template>

<script>

import modals from '@/components/UI/Modal.vue'
import modalRegistration from '@/components/Auth/Registration.vue'
import modalLogin from '@/components/Auth/Login.vue'

export default {
  components: { modals, modalRegistration, modalLogin },
	data () {
		return {
			auth: null,
			login: true,
			register: true
		}
	},
	methods: {
		
	}
}
</script>
