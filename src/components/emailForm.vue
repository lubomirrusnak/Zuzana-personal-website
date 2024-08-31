<template>
    <div class="container">
            <form @submit.prevent="sendEmail">
                <h1>Contact me</h1>
              <div class="form-item">
                
                  <label>Name</label>
                  <input class="name" 
                    type="text" 
                    v-model="name"
                    name="name"
                    placeholder="Your Name"
                  >
              </div>
    
              <label>Email</label>
              <div class="form-item">
                <input 
                  type="email" 
                  v-model="email"
                  name="email"
                  placeholder="Your Email"
                  >
                </div>
              <label>Message</label>
              <div class="form-item">
                  <textarea 
                    name="message"
                    v-model="message"
                    cols="30" rows="5"
                    placeholder="Message">
                  </textarea>
              </div>
              <input type="submit" value="Send">
            </form>
        </div>
    
    </template>
    
    <script>
    import emailjs from '@emailjs/browser';

    
        export default {
            name: 'ContactUs',
      data() {
        return {
          
          name: '',
          email: '',
          message: ''
        }
      },
      methods: {
    
        sendEmail(e) {
          try {
            emailjs.sendForm('service_qehc9fc', 'template_3x5465r', e.target, 'DF_4XP1Y4OGV5bTyV', {
              name: this.name,
              email: this.email,
              message: this.meessage
            })
    
          } catch (err) {
               if (err instanceof ReferenceError) {
                alert( "JSON Error: " + err.message );
               } else {
                throw err; // rethrow
               }
          }
          // Reset form field
          this.name = ''
          this.email = ''
          this.message = ''
        },
      }
    }
    </script>
    
    <style >
    /*formular*/
    * {
      box-sizing: border-box;
      border-radius: 30px;
     
    }
    .form-item{
      margin-bottom: 40px; /* Medzera medzi položkami */
      /*border: 2px solid red;*/ /* nastaví rámček so šírkou 2 pixely a farbou žltou */
      /*padding: 5px; *//* pridá vnútorný okraj okolo textu v rámci rámčeka */
    
    
    }
    
    h1{
      color: wheat;
      margin-bottom:5%
      
    }
    
    label {
      float: left;
      color: wheat;
    }
    input[type=text], [type=email], textarea {
      width: 100%;
      padding: 20px;
      border: 1px solid #ccc;
      border-radius: 10px;
      box-sizing: border-box;
      margin-top: 2px;
      margin-bottom: 14px;
      resize: vertical;
      
    }
    
    input[type=submit] {
      background-color: #9286c4;
      color: white;
      padding: 20px 20px;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      border-radius: 10px;
    }
    
    input[type=submit]:hover {
      background-color: #b8c7b9;
    }
    
    .container {
      display: block;
      margin-top:140px;
      margin-left:25% ;
    
      text-align: center;
      border-radius: 10px;
      padding: 20px;
      width: 50%;
      
      
    }
    
    </style>