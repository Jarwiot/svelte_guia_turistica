<script>
  import { onMount } from 'svelte';
  
  // Lista de destinos turísticos en Jalisco
  const destinos = [
    {
      id: 1,
      nombre: "Guadalajara",
      descripcion: "La capital de Jalisco, conocida como la Perla Tapatía. Visita la Catedral, el Teatro Degollado, el Hospicio Cabañas (Patrimonio de la Humanidad) y disfruta de la gastronomía local.",
      imagen: "https://offloadmedia.feverup.com/guadalajarasecreta.com/wp-content/uploads/2024/06/17133115/Fotos-Wordpress-71.jpg"
    },
    {
      id: 2,
      nombre: "Puerto Vallarta",
      descripcion: "Hermoso destino de playa con aguas cristalinas del Pacífico. Disfruta del Malecón, las playas, los tours en barco y la vibrante vida nocturna.",
      imagen: "https://www.velasvallarta.com.mx/resourcefiles/inner-hero-img/top-attractions-hero-st-min.jpg"
    },
    {
      id: 3,
      nombre: "Tequila",
      descripcion: "Pueblo Mágico donde se produce la famosa bebida mexicana. Visita las destilerías, recorre los campos de agave azul y viaja en el Tequila Express.",
      imagen: "https://visitjalisco.mx/wp-content/uploads/2024/02/andador-tequila-blog.jpg"
    },
    {
      id: 4,
      nombre: "Chapala",
      descripcion: "Hogar del lago más grande de México. Disfruta de paseos en barco, la tranquilidad de sus pueblos ribereños y su agradable clima durante todo el año.",
      imagen: "https://visitagdl.com/wp-content/uploads/2025/03/Portada-Chapala.jpg"
    },
    {
      id: 5,
      nombre: "Tapalpa",
      descripcion: "Pueblo Mágico en la sierra con arquitectura colonial, cascadas, bosques de pino y actividades al aire libre como tirolesas y cabalgatas.",
      imagen: "https://www.journeygourmet.com/continentes/America_Norte/Mexico/Jalisco/Tapalpa/imagenBig.jpg"
    }
  ];

  // Estado para el destino seleccionado
  let destinoSeleccionado = null;
  
  // Función para mostrar detalles de un destino
  function mostrarDestino(destino) {
    destinoSeleccionado = destino;
    window.scrollTo({
      top: document.getElementById('detalles').offsetTop - 100,
      behavior: 'smooth'
    });
  }
  
  // Función para cerrar los detalles
  function cerrarDetalles() {
    destinoSeleccionado = null;
  }
  
  // Para efectos de animación al cargar
  let cargado = false;
  onMount(() => {
    setTimeout(() => {
      cargado = true;
    }, 100);
  });
</script>

<main class="min-h-screen bg-amber-50">
  <!-- Encabezado -->
  <header class="bg-gradient-to-r from-yellow-600 to-red-700 text-white shadow-lg">
    <div class="container mx-auto px-4 py-6">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <h1 class="text-4xl font-bold mb-4 md:mb-0">Descubre Jalisco</h1>
        <nav>
          <ul class="flex space-x-6">
            <li><a href="#destinos" class="hover:text-yellow-200 transition-colors">Destinos</a></li>
            <li><a href="#acerca" class="hover:text-yellow-200 transition-colors">Acerca de</a></li>
            <li><a href="#contacto" class="hover:text-yellow-200 transition-colors">Contacto</a></li>
          </ul>
        </nav>
      </div>
    </div>
  </header>

  <!-- Banner principal -->
  <section class="relative h-96 bg-cover bg-center" style="background-image: url('https://upload.wikimedia.org/wikipedia/commons/thumb/7/70/Guadalajara%2C_PH.jpg/1200px-Guadalajara%2C_PH.jpg')">
    <div class="absolute inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div class="text-center text-white px-4">
        <h2 class="text-5xl font-bold mb-4 transition-transform transform {cargado ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'}" style="transition-duration: 1s;">
          Jalisco: Tierra de Tradición y desarollo
        </h2>
        <p class="text-xl max-w-2xl mx-auto transition-transform transform {cargado ? 'translate-y-0 opacity-100' : 'translate-y-10 opacity-0'}" style="transition-duration: 1s; transition-delay: 0.3s;">
          Descubre la riqueza cultural, natural y gastronómica del estado que dio al mundo el tequila, el mariachi y la charrería.
        </p>
      </div>
    </div>
  </section>

  <!-- Sección de destinos -->
  <section id="destinos" class="py-16 container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12 text-red-800">Destinos Turísticos Imperdibles</h2>
    
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
      {#each destinos as destino, i}
        <div 
          class="bg-white rounded-lg overflow-hidden shadow-lg hover:shadow-xl transition-all transform hover:-translate-y-2 cursor-pointer"
          on:click={() => mostrarDestino(destino)}
          style="transition-delay: {i * 0.1}s"
        >
          <div class="h-48 bg-gray-300 relative">
            <img 
              src={destino.imagen || "/placeholder.svg"} 
              alt={destino.nombre}
              class="w-full h-full object-cover"
            />
          </div>
          <div class="p-6">
            <h3 class="text-xl font-bold mb-2 text-red-700">{destino.nombre}</h3>
            <p class="text-gray-700 line-clamp-3">{destino.descripcion}</p>
            <button class="mt-4 px-4 py-2 bg-yellow-600 text-white rounded hover:bg-yellow-700 transition-colors">
              Ver más
            </button>
          </div>
        </div>
      {/each}
    </div>
  </section>

  <!-- Sección de detalles del destino -->
  <section id="detalles" class="py-8 container mx-auto px-4">
    {#if destinoSeleccionado}
      <div class="bg-white rounded-lg shadow-xl p-6 animate-fade-in">
        <div class="flex justify-between items-start mb-4">
          <h2 class="text-3xl font-bold text-red-800">{destinoSeleccionado.nombre}</h2>
          <button 
            on:click={cerrarDetalles}
            class="text-gray-500 hover:text-red-700 transition-colors"
          >
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>
        </div>
        
        <div class="flex flex-col md:flex-row gap-6">
          <div class="md:w-1/2">
            <img 
              src={destinoSeleccionado.imagen || "/placeholder.svg"} 
              alt={destinoSeleccionado.nombre}
              class="w-full h-auto rounded-lg"
            />
          </div>
          <div class="md:w-1/2">
            <p class="text-gray-700 mb-4">{destinoSeleccionado.descripcion}</p>
            <p class="text-gray-700 mb-4">
              Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vivamus lacinia odio vitae vestibulum vestibulum. Cras porttitor metus in nibh finibus, a volutpat nisi pretium. Nam facilisis, justo ut posuere tempus.
            </p>
            <div class="mt-6">
              <h3 class="text-xl font-bold mb-2 text-red-800">Actividades recomendadas:</h3>
              <ul class="list-disc pl-5 text-gray-700">
                <li>Visitar los principales monumentos y atracciones</li>
                <li>Probar la gastronomía local</li>
                <li>Comprar artesanías tradicionales</li>
                <li>Participar en tours guiados</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    {/if}
  </section>

  <!-- Acerca de Jalisco -->
  <section id="acerca" class="py-16 bg-red-700 text-white">
    <div class="container mx-auto px-4">
      <h2 class="text-3xl font-bold text-center mb-8">Acerca de Jalisco</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
        <div>
          <p class="mb-4">
            Jalisco es uno de los estados más emblemáticos de México, cuna de tradiciones que han trascendido fronteras como el mariachi, la charrería y el tequila.
          </p>
          <p class="mb-4">
            Con una superficie de 78,588 km², Jalisco ofrece una gran diversidad de paisajes: desde playas paradisíacas en la costa del Pacífico, hasta bosques de pino en la sierra, pasando por el impresionante Cañón de Bolaños y el Lago de Chapala, el más grande de México.
          </p>
          <p>
            Su capital, Guadalajara, es la segunda ciudad más grande del país y un importante centro cultural, económico y turístico.
          </p>
        </div>
        <div class="flex justify-center items-center">
          <div class="bg-white p-4 rounded-lg shadow-lg">
            <img 
              src="https://travelifyou.com/wp-content/uploads/2023/08/agave-field-for-tequila-production-jalisco-mexico-1536x1024.jpg" 
              alt="Mapa de Jalisco"
              class="w-full h-auto rounded"
            />
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- Sección de gastronomía -->
  <section class="py-16 container mx-auto px-4">
    <h2 class="text-3xl font-bold text-center mb-12 text-red-800">Gastronomía Jalisciense</h2>
    
    <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
      <div class="bg-white rounded-lg shadow-lg overflow-hidden">
        <img 
          src="https://usa.sopitas.com/wp-content/uploads/sites/2/2023/03/Torta-Ahogada-portada.jpeg" 
          alt="Torta Ahogada"
          class="w-full h-48 object-cover"
        />
        <div class="p-6">
          <h3 class="text-xl font-bold mb-2 text-red-700">Torta Ahogada</h3>
          <p class="text-gray-700">
            Sándwich o "lonche" de cerdo "ahogado" en salsa de chile picante, es el platillo más emblemático de Guadalajara.
          </p>
        </div>
      </div>
      
      <div class="bg-white rounded-lg shadow-lg overflow-hidden">
        <img 
          src="https://images.unsplash.com/photo-1514362545857-3bc16c4c7d1b?q=80&w=2070&auto=format&fit=crop" 
          alt="Tequila"
          class="w-full h-48 object-cover"
        />
        <div class="p-6">
          <h3 class="text-xl font-bold mb-2 text-red-700">Tequila</h3>
          <p class="text-gray-700">
            La bebida nacional de México, producida a partir del agave azul que crece en la región.
          </p>
        </div>
      </div>
      
      <div class="bg-white rounded-lg shadow-lg overflow-hidden">
        <img 
          src="https://cocinamia.com.mx/wp-content/uploads/2018/12/birria-1100x500.png" 
          alt="Birria"
          class="w-full h-48 object-cover"
        />
        <div class="p-6">
          <h3 class="text-xl font-bold mb-2 text-red-700">Birria</h3>
          <p class="text-gray-700">
            Guiso tradicional de carne de chivo o res, cocinado lentamente con chiles y especias.
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Contacto -->
  <section id="contacto" class="py-16 bg-amber-100">
    <div class="container mx-auto px-4">
      <h2 class="text-3xl font-bold text-center mb-8 text-red-800">Contacto</h2>
      
      <div class="max-w-md mx-auto bg-white rounded-lg shadow-lg p-6">
        <form class="space-y-4">
          <div>
            <label for="nombre" class="block text-gray-700 mb-2">Nombre</label>
            <input 
              type="text" 
              id="nombre" 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-600"
              placeholder="Tu nombre"
            />
          </div>
          
          <div>
            <label for="email" class="block text-gray-700 mb-2">Email</label>
            <input 
              type="email" 
              id="email" 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-600"
              placeholder="tu@email.com"
            />
          </div>
          
          <div>
            <label for="mensaje" class="block text-gray-700 mb-2">Mensaje</label>
            <textarea 
              id="mensaje" 
              rows="4" 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-yellow-600"
              placeholder="¿Qué te gustaría saber sobre Jalisco?"
            ></textarea>
          </div>
          
          <button 
            type="submit" 
            class="w-full bg-yellow-600 text-white py-2 px-4 rounded-lg hover:bg-yellow-700 transition-colors"
          >
            Enviar mensaje
          </button>
        </form>
      </div>
    </div>
  </section>

  <!-- Pie de página -->
  <footer class="bg-red-900 text-white py-8">
    <div class="container mx-auto px-4">
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div>
          <h3 class="text-xl font-bold mb-4">Descubre Jalisco</h3>
          <p>Tu guía completa para explorar las maravillas de Jalisco, México.</p>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-4">Enlaces rápidos</h3>
          <ul class="space-y-2">
            <li><a href="#destinos" class="hover:text-yellow-200 transition-colors">Destinos</a></li>
            <li><a href="#acerca" class="hover:text-yellow-200 transition-colors">Acerca de</a></li>
            <li><a href="#contacto" class="hover:text-yellow-200 transition-colors">Contacto</a></li>
          </ul>
        </div>
        
        <div>
          <h3 class="text-xl font-bold mb-4">Síguenos</h3>
          <div class="flex space-x-4">
            <a href="#" class="hover:text-yellow-200 transition-colors">
              <span class="sr-only">Facebook</span>
              <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M22 12c0-5.523-4.477-10-10-10S2 6.477 2 12c0 4.991 3.657 9.128 8.438 9.878v-6.987h-2.54V12h2.54V9.797c0-2.506 1.492-3.89 3.777-3.89 1.094 0 2.238.195 2.238.195v2.46h-1.26c-1.243 0-1.63.771-1.63 1.562V12h2.773l-.443 2.89h-2.33v6.988C18.343 21.128 22 16.991 22 12z" clip-rule="evenodd" />
              </svg>
            </a>
            <a href="#" class="hover:text-yellow-200 transition-colors">
              <span class="sr-only">Instagram</span>
              <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path fill-rule="evenodd" d="M12.315 2c2.43 0 2.784.013 3.808.06 1.064.049 1.791.218 2.427.465a4.902 4.902 0 011.772 1.153 4.902 4.902 0 011.153 1.772c.247.636.416 1.363.465 2.427.048 1.067.06 1.407.06 4.123v.08c0 2.643-.012 2.987-.06 4.043-.049 1.064-.218 1.791-.465 2.427a4.902 4.902 0 01-1.153 1.772 4.902 4.902 0 01-1.772 1.153c-.636.247-1.363.416-2.427.465-1.067.048-1.407.06-4.123.06h-.08c-2.643 0-2.987-.012-4.043-.06-1.064-.049-1.791-.218-2.427-.465a4.902 4.902 0 01-1.772-1.153 4.902 4.902 0 01-1.153-1.772c-.247-.636-.416-1.363-.465-2.427-.047-1.024-.06-1.379-.06-3.808v-.63c0-2.43.013-2.784.06-3.808.049-1.064.218-1.791.465-2.427a4.902 4.902 0 011.153-1.772A4.902 4.902 0 015.45 2.525c.636-.247 1.363-.416 2.427-.465C8.901 2.013 9.256 2 11.685 2h.63zm-.081 1.802h-.468c-2.456 0-2.784.011-3.807.058-.975.045-1.504.207-1.857.344-.467.182-.8.398-1.15.748-.35.35-.566.683-.748 1.15-.137.353-.3.882-.344 1.857-.047 1.023-.058 1.351-.058 3.807v.468c0 2.456.011 2.784.058 3.807.045.975.207 1.504.344 1.857.182.466.399.8.748 1.15.35.35.683.566 1.15.748.353.137.882.3 1.857.344 1.054.048 1.37.058 4.041.058h.08c2.597 0 2.917-.01 3.96-.058.976-.045 1.505-.207 1.858-.344.466-.182.8-.398 1.15-.748.35-.35.566-.683.748-1.15.137-.353.3-.882.344-1.857.048-1.055.058-1.37.058-4.041v-.08c0-2.597-.01-2.917-.058-3.96-.045-.976-.207-1.505-.344-1.858a3.097 3.097 0 00-.748-1.15 3.098 3.098 0 00-1.15-.748c-.353-.137-.882-.3-1.857-.344-1.023-.047-1.351-.058-3.807-.058zM12 6.865a5.135 5.135 0 110 10.27 5.135 5.135 0 010-10.27zm0 1.802a3.333 3.333 0 100 6.666 3.333 3.333 0 000-6.666zm5.338-3.205a1.2 1.2 0 110 2.4 1.2 1.2 0 010-2.4z" clip-rule="evenodd" />
              </svg>
            </a>
            <a href="#" class="hover:text-yellow-200 transition-colors">
              <span class="sr-only">Twitter</span>
              <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
                <path d="M8.29 20.251c7.547 0 11.675-6.253 11.675-11.675 0-.178 0-.355-.012-.53A8.348 8.348 0 0022 5.92a8.19 8.19 0 01-2.357.646 4.118 4.118 0 001.804-2.27 8.224 8.224 0 01-2.605.996 4.107 4.107 0 00-6.993 3.743 11.65 11.65 0 01-8.457-4.287 4.106 4.106 0 001.27 5.477A4.072 4.072 0 012.8 9.713v.052a4.105 4.105 0 003.292 4.022 4.095 4.095 0 01-1.853.07 4.108 4.108 0 003.834 2.85A8.233 8.233 0 012 18.407a11.616 11.616 0 006.29 1.84" />
              </svg>
            </a>
          </div>
        </div>
      </div>
      
      <div class="mt-8 pt-8 border-t border-red-800 text-center">
        <p>&copy; {new Date().getFullYear()} Descubre Jalisco. Todos los derechos reservados.</p>
      </div>
    </div>
  </footer>
</main>

<style>
  /* Animaciones adicionales */
  .animate-fade-in {
    animation: fadeIn 0.5s ease-in-out;
  }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  /* Estilos para limitar líneas de texto */
  .line-clamp-3 {
    display: -webkit-box;
    -webkit-line-clamp: 3;
    -webkit-box-orient: vertical;
    overflow: hidden;
  }
</style>