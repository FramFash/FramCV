<script lang="ts">
  import { base } from '$app/paths';
  import Pbar from '$lib/components/Pbar.svelte';
  const currentDate: Date = new Date(Date.now()); 
  const birthDay: Date = new Date(1995, 12, 11);

  let diff = (currentDate.getTime() - birthDay.getTime()) / 1000;
  diff /= (60 * 60 * 24);

  const age = Math.abs(Math.round(diff / 365.25));

  const sd = currentDate.getFullYear() - 2023;
  const db = currentDate.getFullYear() - 2024;
  const dc = currentDate.getFullYear() - 2024;
  const it = currentDate.getFullYear() - 2024;

  const scul = currentDate.getFullYear() - 2020;
</script>
<div class="main-container">
  <h2>Adolfo Almazán Becerril</h2>
  <div class="info-card">
    <div class="personal-info">
      <p>
        El mundo de la tecnología está siempre cambiando y es imposible conocer todas las plataformas,
        lenguajes, librerías y frameworks existentes pero soy un fanático de estudiar y todo se puede aprender
        con esfuerzo y dedicación.
      </p>

      <h4>Experiencia</h4>
      <ul>
        <li>{sd} años de experiencia como desarrollador de software</li>
        <li>{db} año de experiencia administrando bases de datos en producción</li>
        <li>{dc} año de experiencia en ciencia de datos</li>
        <li>{it} año de experiencia como ingeniero en sistemas</li>
      </ul>

      <p>
        Mi misión trabajando con empresas es involucrarme profundamente con su funcionamiento y conocer sus
        procesos y sistemas para ofrecer la mejor solución posible a sus problemas con la esperanza de 
        lograr un cambio significativo en el funcionamiento de la empresa así como la calidad de vida de 
        las personas.
      </p>
    </div>
    <div class="basic-data">
      <h4>Educación</h4>
      <p>
        Mi educación conciste de casi {scul} años estudiando Ingenieria de Software con una especialización
        en Ingeniería de Datos y Ciencia de datos, alrededor de 50 certificados de cursos de los siguientes temas:        
      </p>
      <ul>
        <li>Ingeniería de Software</li>
        <li>Ingeniería en Sistemas</li>
        <li>CyberSeguridad</li>
        <li>Ciencia de Datos</li>
        <li>Lenguajes de Programación</li>
        <li>Organización de Emprezas</li>
        <li>Inteligencia Artificial y Machine Learning</li>
        <li>Tecnologías en la Nube</li>
        <li>Desarrollo Front-End, Back-End y Full-Stack</li>
        <li>Pentesting y Hackeo Ético</li>
      </ul>
    </div>
  </div>
    <div class="statistics">
      <h3>Habilidades Técnicas</h3>
      <div class="skill">
        <h4>HTML</h4>
        <Pbar progress=70/>
      </div>
      <div class="skill">
        <h4>CSS</h4>
        <Pbar progress=70/>
      </div>
      <div class="skill">
        <h4>Rust</h4>
        <Pbar progress=80/>
      </div>
      <div class="skill">
        <h4>JavaScript</h4>
        <Pbar progress=40/>
      </div>
      <div class="skill">
        <h4>Golang</h4>
        <Pbar progress=30/>
      </div>
      <div class="skill">
        <h4>Flutter</h4>
        <Pbar progress=40/>
      </div>
      <div class="skill">
        <h4>Svelte</h4>
        <Pbar progress=70/>
      </div>
      <div class="skill">
        <h4>Python</h4>
        <Pbar progress=70/>
      </div>
      <div class="skill">
        <h4>Closure</h4>
        <Pbar progress=20/>
      </div>
      <div class="skill">
        <h4>C / C++</h4>
        <Pbar progress=50/>
      </div>
      <div class="skill">
        <h4>Bash</h4>
        <Pbar progress=60/>
      </div>
      <div class="skill">
        <h4>Git</h4>
        <Pbar progress=50/>
      </div>
    </div>
    <div class="other-exp">
      <h3>Experiencia en otros Ámbitos</h3>
      <div class="info-card-alt">
        <h4>Educación en las Artes</h4>
        <p>
          La primera educación profesional que tuve fué en el ámbito de las artes escenicas, esto incluye
          3 años estudiando actuación en el instituto Andrés Soler, 2 años estudiando Ballet en el Instituto
          Andrés Soler y 12 años estudiando violín y composición en varias escuelas como Gmartell y ESMUC en Barcelona.
        </p>
        <p>
          Esta educación mientras que no está relacionada con el mundo de la tecnología, estadistica e infraestructura
          me enseñó multiples cualidades que considero son de utilidad en el mundo de los sistemas, cualidades como
          la diciplina, puntualidad, organización que son habilidades importantes a la hora de trabajar con gente,
          Así como el lado creativo a la hora de proponer ideas alternativas, resolución de problemas y un enfoque
          más humano a la hora de desarrollar una aplicación o sistema con el que los clientes van a trabajar por horas.
         </p>
         <h4>Animación y Modelado 3D</h4>
         <p>
           Por gusto personal y en mis tiempos libres he aprendido a usar herramientas como Blender, Unreal Engine,
           Godot, Bevy, Manim, entre otras que son herramientas muy utiles a la hora de tratar de comunicar visualmente
           alguna idea o concepto para otro tipo de projectos en los que un producto tangible es el que se está ofreciendo
           y visualizarlo es de suma importancia. 
         </p>
         <h4>Ingenieria en Audio</h4>
         <p>
           Como parte de mis estudios en la Música gran cantidad de preparación también estuvo dirigida a saber
           usar equipo de audio para eventos, grabación y todo timpo de situaciónes en las que algún tipo de sonido
           analogo o digital esté involucrado, herramientas de este ámbito que se usar son Ableton, LogicPro, Musescore,
           Sibelius y también el uso de hardware de audio como Mezcladoras, Amplificadores, Splitters, Monitoreo, Microfoneo, entre otras.
         </p>
      </div>
    </div>
    <div class="statistics">
      <h3>Lenguages</h3>
      <div class="skill">
        <h4>Inglés</h4>
        <Pbar progress=80/>
      </div>
      <div class="skill">
        <h4>Alemán</h4>
        <Pbar progress=40/>
      </div>
      <div class="skill">
        <h4>Italiano</h4>
        <Pbar progress=50/>
      </div>
      <div class="skill">
        <h4>Japones</h4>
        <Pbar progress=20/>
      </div>
      <div class="skill">
        <h4>Coreano</h4>
        <Pbar progress=30/>
      </div>
    </div>
</div>
<style>
  .main-container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    & h2 {
      color: white;
      margin-top: 10rem;
    }
  }

  .info-card {
    margin-top: 1rem;
    width: 90%;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    border-radius: 5px;
    box-shadow: 0 0 10px 2px #F05F57;
    display: grid;
    grid-template-columns: 50% 50%;
  }

  .other-exp {
    width: 90%;
    grid-column: 1 / 3;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .info-card-alt {
    padding: 1rem;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    border-radius: 5px;
    box-shadow: 0 0 10px 2px #F05F57;
  }

  .personal-info {
    padding: 1rem;
    grid-column: 1 / 2;
  }

  .basic-data {
    grid-column: 2 / 3;
    display: flex;
    flex-direction: column;
    align-items:flex-start;
  }

.statistics {
  margin: 2rem 0;
  width: 90%;
  display: grid;
  grid-template-columns: 50% 50%;
  gap: 1rem;

  & h3 {
    grid-column: 1 / 3;
    margin: auto;
  }
}

.skill {
  height: 4rem;
  display: grid;
  grid-template-columns: 20% 80%;
  border-radius: 5px;
  transition: 0.5s;
  background-size: 200% auto;
  color: white;            
  box-shadow: 0 0 10px 2px white;

  & h4 {
    margin: auto;
  }
}

@media (max-width: 500px) {
  .main-container h2 {
    margin-top: 6rem;
  }
  .statistics {
    gap: 0.5rem;
  }
  .skill {
    font-size: 0.6rem;
    box-shadow: 0 0 5px 1px white;
    & h4 {
      margin-left: 0.5rem;
    }
  }
  .info-card {
    margin-top: 1rem;
    width: 100%;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    border-radius: 0px;
    box-shadow: 0 0 5px 1px #F05F57;
    display: grid;
    grid-template-columns: 100%;
  }
  .basic-data {
    margin: 10px;
    grid-column: 1/2;
    display: flex;
    flex-direction: column;
    align-items:flex-start;
  }
  .other-exp {
    width: 100%;
  }
  .info-card-alt {
    border-radius: 0;
    box-shadow: 0 0 5px 1px #F05F57;
  }
}
</style>
