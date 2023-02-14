<template>
  <section class="bg-white shadow section">
    <div class="container mx-auto">
      <div class="flex flex-col md:flex-row md:justify-center">
        <div class="md:w-1/3">
          <h2 class="text-3xl font-bold text-center mb-8">Reset Password</h2>

          <Notification :message="error" v-if="error"/>

          <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4" method="post" @submit.prevent="submitForm">
            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2" for="email">
                Email
              </label>
              <div class="control">
                <input
                  type="email"
                  class="input w-full px-4 py-2 border rounded"
                  name="email"
                  @input="checkEmail"
                  v-model="email"
                  placeholder="Email Address"
                />
              </div>
            </div>
            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2" for="password">
                Password
              </label>
              <div>
                <ul class="flex flex-col">
                  <li :class="{ 'is_valid': contains_eight_characters }">8 Characters</li>
                  <li :class="{ 'is_valid': contains_number }">Contains Number</li>
                  <li :class="{ 'is_valid': contains_uppercase }">Contains Uppercase</li>
                  <li :class="{ 'is_valid': contains_special_character }">Contains Special Character</li>
                </ul>

                <div class="checkmark_container" :class="{ 'show_checkmark': valid_password }">
                  <svg width="50%" height="50%" viewBox="0 0 140 100">
                    <path class="checkmark" :class="{ 'checked': valid_password }" d="M10,50 l25,40 l95,-70" />
                  </svg>
                </div>
              </div>

              <div class="control">
                <input
                  type="password"
                  @input="checkPassword"
                  class="input w-full px-4 py-2 border rounded"
                  name="password"
                  v-model="password"
                  autocomplete="off"
                  placeholder="Password"
                />
              </div>
            </div>
            <div class="control">
              <nuxt-link to="/confirmation">
                <button type="submit" class="bg-gray-900 hover:bg-gray-800 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" @click="handleLinkClick">Change</button>

              </nuxt-link>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

  
  <script>
  import VueSweetalert2 from 'vue-sweetalert2';
  import 'sweetalert2/dist/sweetalert2.min.css';
  import Swal from 'sweetalert2'

export default {


  name: 'RegisterUser',
  data () {
    return {
      email: '',
      password: '',
      email: null,
      password: null,
      password_length: 0,
      contains_eight_characters: false,
      contains_number: false,
      contains_uppercase: false,
      contains_special_character: false,
      valid_password: false,
      valid_email: false,
      error: null
    }
  },
  methods: { 
    handleLinkClick() {
    if (!this.valid_password || !this.valid_email) {
      event.preventDefault(); 
      Swal.fire({
           title: 'Error',
           text: 'Please complete both email and password fields.',
           icon: 'error',
           confirmButtonText: 'OK'
         });
         return;
    }
    // Other code to handle the link click
  },
    checkPassword() {
      this.password_length = this.password.length;
      const format = /[ !@#$%^&*()_+\-=\[\]{};':"\\|,.<>\/?]/;

      if (this.password_length > 8) {
        this.contains_eight_characters = true;
      } else {
        this.contains_eight_characters = false;
      }

      this.contains_number = /\d/.test(this.password);
      this.contains_uppercase = /[A-Z]/.test(this.password);
      this.contains_special_character = format.test(this.password);

      if (this.contains_eight_characters === true &&
          this.contains_special_character === true &&
          this.contains_uppercase === true &&
          this.contains_number === true) {
        this.valid_password = true;
      } else {
        this.valid_password = false;
      }
    },
    checkEmail() {
      const emailFormat = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;

      if (!this.email.match(emailFormat)) {
        this.valid_email = false;
      } else {
        this.valid_email = true;
      }
    },
    submitForm() {
  if (!this.valid_email) {
    this.error = "Invalid email address.";
    return;
  }
  if (!this.valid_password) {
    this.error = "Password does not meet the required criteria.";
    return;
  }
  this.handleChange();
},
      // Perform your submit logic here
      // ...

     
    }
  }
</script>
<style>


h2 {
	text-align: center;
	color: #FFF;
	font-weight: 400;
}

ul {
	padding-left: 20px;
	display: flex;
	flex-direction: column;
	align-items: flex-start;
}

li { 
	margin-bottom: 8px;
	color: #525f7f;
	position: relative;
}

li:before {
  content: "";
	width: 0%; height: 2px;
	background: #2ecc71;
	position: absolute;
	left: 0; top: 50%;
	display: block;
	transition: all .6s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

#app { width: 400px; }


/* Password Input --------- */

.input_container {
	position: relative;
	padding: 30px;
	box-shadow: 0 10px 20px rgba(0,0,0,0.19), 0 6px 6px rgba(0,0,0,0.23);
	border-radius: 6px;
	background: #FFF;
}

input[type="password"] {
	line-height: 1.5;
	display: block;
	color: rgba(136, 152, 170, 1);
	font-weight: 300;
	width: 100%;
	height: calc(2.75rem + 2px);
	padding: .625rem .75rem;
	border-radius: .25rem;
	background-color: #fff;
	transition: border-color .4s ease;
	border: 1px solid #cad1d7;
	outline: 0;
}

input[type="password"]:focus {
	border-color: rgba(50, 151, 211, .45);
}


/* Checkmark & Strikethrough --------- */

.is_valid { color: rgba(136, 152, 170, 0.8); }
.is_valid:before { width: 100%; }

.checkmark_container {
	border-radius: 50%;
	position: absolute;
	top: -15px; right: -15px;
	background: #2ecc71;
	width: 50px; height: 50px;
	visibility: hidden;
	opacity: 0;
	display: flex;
	justify-content: center;
	align-items: center;
	transition: opacity .4s ease;
}

</style>
