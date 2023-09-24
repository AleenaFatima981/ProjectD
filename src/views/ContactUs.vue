



<template>
    <div class="contact-bg">
      <div class="container mt-5">
        <div class="row justify-content-center">
          <div class="col-md-6">
            <form class="p-4 border rounded contact-form">
              <h2 class="mb-4">Contact Me Form</h2>
  
              <div class="mb-3">
                <label for="name" class="form-label">Name:</label>
                <input v-model="name" id="name" class="neu-input" />
              </div>
  
              <div class="mb-3">
                <label for="email" class="form-label">Email:</label>
                <input v-model="email" id="email" class="neu-input" type="email" />
              </div>
  
              <div class="mb-3">
                <label for="password" class="form-label">Password:</label>
                <input v-model="password" id="password" class="neu-input" type="password" />
              </div>
  
              <div class="mb-3">
                <label for="address" class="form-label">Address:</label>
                <textarea v-model="address" id="address" class="neu-input" rows="3"></textarea>
              </div>
  
              <div class="form-check mb-3">
                <input v-model="termsAgreed" class="hidden-checkbox" type="checkbox" id="termsAgreed" />
                <label class="custom-checkbox" for="termsAgreed"></label>
                <label class="form-check-label ml-4" for="termsAgreed">I agree to the terms of service</label>
              </div>
  
              <button @click="register" :disabled="!isValid" class="neu-btn">Register</button>
            </form>
            <div class="bar-chart mt-5">
              <div class="bar" :style="{ height: nameLength + 'px' }">Name Length score: {{ nameLength }}</div>
              <div class="bar" :style="{ height: emailLength + 'px' }">Email Length score: {{ emailLength }}</div>
              <div class="bar" :style="{ height: passwordLength + 'px' }">Password Length: {{ passwordLength }}</div>
              <div class="bar" :style="{ height: addressLength + 'px' }">Address Length: {{ addressLength }}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { computed } from 'vue';
  
  export default {
    data() {
      return {
        name: "",
        email: "",
        password: "",
        address: "",
        termsAgreed: false
      };
    },
    computed: {
      isValid() {
        return this.name && this.email && this.password && this.address && this.termsAgreed;
      },
      nameLength() {
        return this.name.length * 10; // multiplied by 10 for better visualization
      },
      emailLength() {
        return this.email.length * 10;
      },
      passwordLength() {
        return this.password.length * 10;
      },
      addressLength() {
        return this.address.length * 10;
      }
    },
    methods: {
      register() {
        if (this.isValid) {
          this.$emit("user.register", {
            name: this.name,
            email: this.email,
            password: this.password,
            address: this.address
          });
        }
      }
    }
  };
  </script>
  
  <style scoped>
  /* Responsive Styles */
@media (max-width: 768px) { /* Phone */
    .container {
        padding: 0 15px; /* Add some padding for better spacing on smaller screens */
    }

    .contact-form {
        padding: 20px; /* Reduce padding on smaller screens */
    }

    .neu-input, .neu-textarea {
        padding: 8px 12px; /* Slightly reduce padding */
    }

    .bar-chart {
        flex-direction: column; /* Stack bars vertically */
        align-items: center;
    }

    .bar {
        margin-bottom: 10px; /* Add space between vertically stacked bars */
    }
}

 .contact-bg {
    background: linear-gradient(120deg, #a1c4fd, #c2e9fb);
    min-height: 100vh;
  }
  
  .contact-form {
  background-color: #faf5f5;
  box-shadow: -5px -5px 10px #fff, 5px 5px 10px #babecc;
  color: #000; /* This changes the text color to black */
}

.contact-form h2, 
.contact-form label { /* This sets the color of h2 and label elements inside the contact form to black */
  color: #000;
}

.form-check-label {
  color: #000; /* This changes the checkbox label text color to black */
}
  
  .neu-input, .neu-textarea {
    background-color: #ececec;
    border: none;
    padding: 10px 15px;
    border-radius: 10px;
    box-shadow: inset -4px -4px 10px #a3a3a3, inset 4px 4px 10px #ffffff;
    width: 100%;
    outline: none;
    transition: all 0.3s ease-in-out;
  }
  
  .neu-input:focus, .neu-textarea:focus {
    box-shadow: inset -2px -2px 5px #a3a3a3, inset 2px 2px 5px #ffffff;
  }
  
  .hidden-checkbox {
    display: none;
  }
  
  .custom-checkbox {
    width: 24px;
    height: 24px;
    background-color: #ececec;
    border-radius: 5px;
    position: relative;
    cursor: pointer;
    box-shadow: -4px -4px 10px #a3a3a3, 4px 4px 10px #ffffff;
    display: inline-block;
  }
  
  .hidden-checkbox:checked + .custom-checkbox {
    background-color: #a1c4fd;
    box-shadow: none;
  }
  
  .custom-checkbox:after {
    content: '';
    position: absolute;
    top: 6px;
    left: 6px;
    width: 12px;
    height: 12px;
    background-color: #ffffff;
    border-radius: 3px;
    opacity: 0;
    transform: scale(0.5);
    transition: all 0.2s;
  }
  
  .hidden-checkbox:checked + .custom-checkbox:after {
    opacity: 1;
    transform: scale(1);
  }
  
  .neu-btn {
    background-color: #ececec;
    border: none;
    padding: 10px 25px;
    border-radius: 25px;
    cursor: pointer;
    box-shadow: -4px -4px 10px #a3a3a3, 4px 4px 10px #ffffff;
    transition: all 0.3s ease-in-out;
  }
  
  .neu-btn:hover {
    box-shadow: -2px -2px 5px #a3a3a3, 2px 2px 5px #ffffff;
  }
  
  .neu-btn:disabled {
    background-color: #d1d1d1;
    cursor: not-allowed;
  }
  
  .bar-chart {
    display: flex;
    justify-content: space-around;
    margin-top: 20px;
  }
  
  .bar {
    width: 50px;
    background-color: #cf6565;
    color: white;
    text-align: center;
    transition: height 0.2s;
  }
  </style>
  