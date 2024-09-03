<template>


  <nav class="subNavigation">
    
    <ul id="subNav">
      <li class="meno">Lubo</li>    
      <li class="bar"
      
        v-for="header in headers"
        :key="header.id"
        :class="{ active: header.id === currentSection }">
        <a href="#" @click.prevent="scrollTo(header.id)">{{ header.name }}</a>
      </li>
    </ul>
  </nav>
  <div class="content">

    <section id="home">

    </section>
    <section id="about">

    </section>
    <section id="contact">
      <EmailForm></EmailForm>
    </section>
  </div>
  
</template>

<script>
import { ref, onMounted } from 'vue';
import EmailForm from './components/emailForm.vue';

export default {
  name: 'ContactUs', // This is the correct place for the component name
  components: {
    EmailForm
  },
  setup() {
    const currentSection = ref();
    const section = ref();
    
    const headers = [
      { id: 'home', name: 'Home' },
      { id: 'about', name: 'About' },
      { id: 'contact', name: 'Contact' }
    ];
    
    onMounted(() => {
      section.value = document.querySelectorAll('section');
      window.addEventListener('scroll', updateScroll);
      updateScroll();
    });
    
    function updateScroll() {
      section.value.forEach((sec) => {
        const top = window.scrollY;
        const offset = sec.offsetTop - 150;
        const height = sec.offsetHeight;
        const id = sec.getAttribute('id');
        
        if (top >= offset && top < offset + height) {
          currentSection.value = id;
        }
      });
    }

    function scrollTo(sectionId) {
      const element = document.getElementById(sectionId);
      if (element) {
        window.scrollTo({
          top: element.offsetTop,
          behavior: 'smooth'
        });
      }
    }
    
    return { currentSection, headers, scrollTo };
  }
}
</script>


<style>

app {
}
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  scroll-behavior: smooth;
  tect-decoration: none;
  font-family: Verdana;
}
nav {
  position: fixed;
  background: rgb(28, 30, 33);
  top: 0;
  right: 0;
  left: 0;
  height:45px;
  box-shadow: 0 2px 6px -6px white;
  border-radius: 0%;
}

ul {
  list-style: none;
  position: relative;
  display: table;
  margin: 0 auto;
}
li {
  display: table-cell;
}

li > a {
  font-weight: bold;
  line-height: 1rem;
  padding: 18px 0 5px 0;
  margin: 0 25px;
  display: block;
  color: white;
  letter-spacing: 0.125rem;
  text-decoration: none;
  transition: all 0.3s ease-in-out;
  font-weight: 400;
  text-transform: uppercase;
}
li > a:hover {
  border-bottom: 2px solid blue;
  
}
.active > a {
  color: rgba(235, 235, 235, 0.6);
  border-bottom: 2px solid blue;
  
}
.content {
  margin-top: 40px;
  
}

section {
  
  min-height: 100vh;
  display: flex;
  justify-content: left;
  align-items: center;
  font-size: 1em;
  font-weight: bolder;
  padding-bottom: 70px;
  text-transform: uppercase;
  
}

</style>
