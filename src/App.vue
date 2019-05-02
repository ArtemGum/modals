<template>
<div class="wrapper">
	<div class="wrapper-content">

		<section>
			<div class="container">

				 <!-- registration modal -->
				<button class="btn btnPrimary" @click="modalRegistration = !modalRegistration">Registration</button>
				<modalRegistration v-show="modalRegistration" @close="modalRegistration = false"/>

				<!-- Login modal -->
				<button class="btn btnPrimary" @click="modalLogin = !modalLogin">Login</button>
				<modalLogin v-show="modalLogin" @close="modalLogin = false" />

			</div>
		</section>
	</div>

</div>

</template>

<script>

import modals from '@/components/UI/Modal.vue'
import modalRegistration from '@/components/ModalRegistration.vue'
import modalLogin from '@/components/ModalLogin.vue'

export default {
  components: { modals, modalRegistration, modalLogin },
	data () {
		return {
			modalRegistration: false,
			modalLogin: false
		}
	},
	methods: {
	}
}
</script>
