<script lang="ts">
  import { base } from "$app/paths";

</script>
<div class="main-container">
  <h4>Ciencia de Datos & Arquitectura de Sistemas — Optimización de Procesos — Soluciones de
Software a Medida</h4>
  <div class="leader-card">
    <h3>
      Resumen de Experiencia:
    </h3>
    <p>
      Ayudo a empresas a automatizar flujos de trabajo, diseñar sistemas de datos escalables y desarrollar
      software personalizado para mejorar eficiencia y toma de decisiones. Mis habilidades integran ciencia de datos,
      ingenierı́a de software y diseño de procesos, garantizando soluciones técnicas y prácticas.
    </p>
    <h3>
      ¿Por Qué Trabajar Conmigo?
    </h3>
    <ul>
      <li>
        Enfoque Integral: Combino profundidad técnica con entendimiento del negocio.
      </li>
      <li>
        Orientado a Eficiencia: Soluciones que reducen trabajo manual y escalan.
      </li>
      <li>
        Independiente & Ágil: Sin sobrecostos; proyectos entregados con Retorno de la inversión claro.
      </li>
    </ul>
  </div>
  <div class="services">
    <h2>Servicios Principales</h2>
    <div class="service-list">
      <ul>
        <h4>
          Arquitectura de Datos e Ingeniería
        </h4>
        <li>Diseño de pipelines, almacenes de datos y marcos de gobernanza.</li>
        <li>Migración de sistemas legacy a plataformas modernas (ERL, nube, analisis en tiempo real)</li>
        <h4>
          Desarrollo de Software a Medida
        </h4>
        <li>Herramientas para automatización, reporting o necesidades específicas.</li>
        <li>Soluciones full-stack (APIs (servidores web), dashboards (herramientas de administrador), integraciónes)</li>
        <h4>
          Optimización de Procesos
        </h4>
        <li>Rediseño de flujos de trabajo para eliminar cuellos de botella.</li>
        <li>Implementación de KPIs (indicadores clave de desempeño) para medir mejoras.</li>
      </ul>
    </div>
    <div class="service-list">
      <ul>
        <h4>
          Ciencia de Datos & Análisis
        </h4>
        <li>Modelos predictivos, análisis estadístico y soluciones de IA/ML.</li>
        <li>"Traducción" de datos para audiencias no técnicas.</li>        
        <h4>
          Arquitectura de Sistemas
        </h4>
        <li>Diseño de infraestructuras IT seguras y escalables.</li>
        <li>Implementaciones en la nube/híbridas con equilibrio costo-rendimiento.</li>      
      </ul>
    </div>

    <h2>Proyectos Previos</h2>
    <div class="proyectos">
      <h4>Plataforma de Monitoreo de Obras Para Puentes y Autopistas Federales</h4>
      <p>
        Se realizó una plataforma compuesta por una base de datos y una aplicación de escritorio
        para hacer un seguimiento de las obras de mantenimiento para estructuras bajo la jurisdicción del cliente.

        para realizar esta aplicación se hizo uso de las siguientes herramientas:
      </p>
      <ul>
        <li>Rust (Lenguaje de Programación)</li>
        <li>Dioxus (librería de desarrollo front end para Rust)</li>
        <li>Python (Lenguaje de Programación, se utilizó para la limpieza, análisis y organización de la información)</li>
        <li>Postgresql (base de datos)</li>
      </ul>
      <p>
        Algunas de las funciones de la aplicación son las siguientes:
      </p>
      <ul>
        <li>Visualizar de manera eficiente la información</li>
        <li>Generar automaticamente informes</li>
        <li>localización GPS exacta de las estructuras</li>
        <li>Gráficas y estadisticas importantes sobre el estado de las estructuras</li>
      </ul>
      <p>
        Se estima que la aplicación reducirá en un 50% las tareas repetitivas como generar informes,
        reducirá el riesgo de pasar por alto situaciones críticas y agilizará el tiempo de respuesta
        para atender estructuras en mal estado.
      </p>
    </div>
    <div class="proyectos">
      <h4>Aplicación Móbil y Web de educación musicál</h4>
      <p>
        Es una aplicación Android y IOs así como una pagina en el navegador que su intención es enseñar
        teoría musical a principiantes, así como dar consejos e información acerca de la industria a la
        gente interesada en hacer una carrera en el gremio

        para realizar está aplicación se utilizaron las siguientes herramientas:
      </p>

      <ul>
       <li>Golang (lenguaje de programación, utilizado para el servidor web)</li>
       <li>javascript/typescript (lenguaje de programación, utilizado para diseño de pagina web)</li>
       <li>Svelte/Sveltekit (framework de javascript para el diseño frontend de la aplicación)</li>
       <li>Flutter (framework de desarrollo para crear la aplicación móbil)</li>
       <li>Dart (Lenguaje de Programación utilizado por Flutter)</li>
       <li>Firebase (Servicio de almacenamiento en la nube utilizado para la base de datos)</li>
       <li>Python (Lenguaje de Programación, utilizado para funcionalidad con Machine Learning e Inteligencia Artificial)</li>
       <li>Rust (Lenguaje de Programación, utilizado para funcionalidad eficiente y que necesita ser "Memory safe")</li>
      </ul>

      <p>
        Esta aplicación se encuentra en desarrollo, pero se estima que una vez en funcionamiento 
        hará de la educación musical un proceso mas eficiente y accesible para cualquier situación económica
        este servicio manejará un chatbot desarrollado con modelos de MachineLearning para dar retroalimentación
        a los usuarios sobre su progreso además de responder a preguntas especificas que tenga el usuario.
      </p>
    </div> 
  </div>
</div>
<style>
  .main-container {
    margin-top: 8rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .leader-card {
    width: 85%;
    padding: 1rem;
    border-radius: 5px;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    box-shadow: 0 0 10px 2px #F05F57;
  }

  .services {
    margin-top: 1rem;
    width: 85%;
    height: 30rem;
    padding: 1rem;
    display: grid;
    grid-template-columns: 50% 50%;
    gap: 2rem;

    & h2 {
      margin: auto;
      grid-column: 1/3;
    }
  }

  .service-list {
    width: 100%;
    border-radius: 5px;
    box-shadow: 0 0 10px 2px white;

    & h4 {
      margin-top: 20px;
      color: #F05F57;
    }
  }

  .proyectos {
    margin-top: 10px;
    width: 100%;
    grid-column: 1 / 3;
    border-radius: 5px;
    background-image: linear-gradient( 135deg, #F05F57 10%, #360940 100%);
    box-shadow: 0 0 10px 2px #F05F57;

    & * {
      margin: 1rem;
    }

  }

  @media (max-width: 500px) {
    .main-container {
      margin-top: 4rem;

      & h4 {
        margin: 10px;
      }
    }
    .services {
      width: 100%;
      gap: 0.5rem;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 0;
    }

    .service-list {
      width: 90%;
    }

    .proyectos {
      margin-top: 20px;
      width: 100%;
      padding: 0;
      border-radius: 0;
      box-shadow: 0 0 5px 1px #F05F57;

      & * {
        margin: 10px;
      }
    }
    .leader-card {
      padding: 0;
      width: 100%;
      border-radius: 0;
      box-shadow: 0 0 5px 1px #F05F57;

      & * {
        margin: 10px;
      }
    }
  }

</style>
