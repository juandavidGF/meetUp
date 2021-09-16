<template>
  <div class="home">
    <section class="hero-image">
      <div class="hero-text">
        <h1>Encuentra planes interesantes con tus amigos o unete a nuevos grupos y conoce personas</h1>
        <router-link class="btn" tag="button" to="/signUp">
          Registrarse
        </router-link>
      </div>
    </section>
    <div class="features">
      <div class="row">
        <p>Crea planes privados para compartir con tus amigos o publicos para conocer personas</p>
        <div>
          <img src="https://images.unsplash.com/photo-1619538036719-af01c2eb1f41?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1301&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Recibe notificaciones de los próximos planes</p>
        <div>
          <img src="https://images.unsplash.com/photo-1605918321755-0b5ffd8a796a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=334&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Obten sugerencias de nuevos lugares y activdades según tus preferencias</p>
        <div>
          <img src="https://images.unsplash.com/photo-1612599537672-64c5f1869280?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=334&q=80" alt="">
        </div>
      </div>
      <div class="row">
        <p>Encuentra eventos que estan sucediendo ahora mismo</p>
        <div>
          <img src="https://images.unsplash.com/photo-1543269865-cbf427effbad?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80" alt="">
        </div>
      </div>
    </div>
    <div class="btn-section">
      <router-link class="cta-2" tag="button" to="/signUp">
        Registrarse
      </router-link>
      <div></div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>

<style>
    body, html {
      height: 100%;
      margin: 0;
      font-family: Arial, Helvetica, sans-serif;
    }

    .hero-image {
      background-image: linear-gradient(rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5)), url("https://images.unsplash.com/photo-1539635278303-d4002c07eae3?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1350&q=80");
      height: 25rem;
      background-position: center;
      background-repeat: no-repeat;
      background-size: cover;
      position: relative;
    }

    .hero-text {
      position: absolute;
      top: 50%;
      left: 30%;
      transform: translate(-20%, -50%);
      color: white;
      margin: 0 -1rem;
    }

    .hero-text > h1 {
      font-size: 25px;
      line-height: 1.5;
    }

    .btn,
    .cta-2 {
      border: none;
      outline: 0;
      display: inline-block;
      padding: 10px 25px;
      color: black;
      background-color: #ddd;
      text-align: center;
      cursor: pointer;
      margin-top: 1rem;
      border-radius: 3px;
    }

    .btn:hover {
      background-color: #555;
      color: white;
    }

    .features {
      margin-bottom: 3rem;
    }

    .row {
      margin: 4rem 1rem;
    }

    .row > p {
      max-width: 400px;
      width: 100%;
      margin: 0 auto 3rem auto;
      font-size: 20px;
      font-weight: 900;
      line-height: 1.5;
    }

    .row > div > img {
      max-width: 400px;
      width: 100%;
      display: block;
      margin-left: auto;
      margin-right: auto;
      object-fit: contain;
      border-radius: 2%;
    }

    .btn-section {
      background-color: black;
      display: flex;
      padding-top: 1rem;
    }

    .cta-2 {
      padding: 0.7rem 1rem 0.7rem 1rem;
      margin-bottom: 15px;
      max-width: 400px;
      width: 90%;
      margin-left: auto;
      margin-right: auto;
      cursor: pointer;
    }

    .cta-2:hover {
      background-color: #555;
      color: white;
    }

    @media only screen and (min-width: 1800px) {
      .hero-text {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        color: white;
        margin: 0 0;
      }
                  
    }

    @media only screen and (min-width: 768px) {
      .hero-image {
        height: 40rem;
      }

      .hero-text > h1 {
        font-size: 50px;
        max-width: 100rem;
      }

      .hero-text button {
        font-size: 25px;
      }

      .features {
        margin-top: 3rem;
        max-width: 1500px;
        margin: 3rem auto 0 auto;
      }

      .row {
        display: flex;
        padding: 10px 0;
      }

      .row:nth-child(even) {
        flex-direction: row-reverse;
      }

      .row > * {
        width: 50%;
      }

      .row > p {
        font-size: 20px;
        max-width: 400px;
        margin: auto auto;
      }

      .row > div > img {
        object-fit: contain;
        max-width: 300px;
        margin-left: auto;
        margin-right: auto;
        border-radius: 2%;
      }

      .row:nth-child(even) > div > img {
        transform: rotate(1deg);
      }

      .row:nth-child(odd) > div > img {
        transform: rotate(2deg);
      }

      .btn-section {
        /* display: flex; */
        /* flex-direction: row; */
        background-color: black;
        margin-top: 7rem;
        padding: 10px 0;
      }

      .cta-2 {
        /* display: flex; */
        /* width: 90%; */
        font-size: 20px;
        margin-left: auto;
        margin-right: auto;
        padding: 1rem;
        margin-bottom: 15px;
      }
    }

  </style>