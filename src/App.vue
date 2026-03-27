<script setup>
import { ref } from 'vue';
import axios from 'axios';

const url = "http://localhost:8080/taller-5/datos_t5.php";

const paciente = ref({
  nombre: '',
  fec_nac: '',
  genero: 'Masculino',
  n_medico: '',
  fec_visita: '',
  g_medicamentos: 'No'
});


const registrarPaciente = async () => {
  try {
    
    const respuesta = await axios.post(url, paciente.value);
    
    if (respuesta.data.success) {
      alert("Servidor dice: " + respuesta.data.message);
      
      // Limpiamos el formulario tras el éxito
      paciente.value = { 
        nombre: '', fec_nac: '', genero: 'Masculino', 
        n_medico: '', fec_visita: '', g_medicamentos: 'No' 
      };
    } else {
      alert("Error en el PHP: " + respuesta.data.error);
    }
  } catch (error) {
    console.error("Error de red:", error);
    alert("No se pudo conectar con XAMPP. Revisa que Apache esté encendido.");
  }
};
</script>


<template>

    <div class="pagina-fondo">
    <div class="contenedor-tarjeta">
      <h2 class="titulo">Captura de Datos del Paciente</h2>
      
      <form @submit.prevent="registrarPaciente">

        <div class="fila-formulario">
          <label>Nombre Completo:</label>
          <input type="text" v-model="paciente.nombre" required placeholder="Ej. Juan Pérez">
        </div>

        <div class="fila-formulario">
          <label>Fecha de Nacimiento:</label>
          <input type="date" v-model="paciente.fec_nac" required>
        </div>

        <div class="fila-formulario">
          <label>Género:</label>
          <select v-model="paciente.genero">
            <option value="Masculino">Masculino</option>
            <option value="Femenino">Femenino</option>
            <option value="Otro">Otro</option>
          </select>
        </div>

        <div class="fila-formulario">
          <label>Nombre Médico:</label>
          <input type="text" v-model="paciente.n_medico" required>
        </div>

        <div class="fila-formulario">
          <label>Fecha de Visita:</label>
          <input type="date" v-model="paciente.fec_visita" required>
        </div>

        <div class="fila-formulario">
          <label>Generó Medicamentos:</label>
          <select v-model="paciente.g_medicamentos">
            <option value="No">No</option>
            <option value="Si">Sí</option>
          </select>
        </div>

        <div class="acciones">
          <button type="submit" class="btn-primario">Registrar Paciente</button>
          <button type="button" class="btn-secundario">Ver Pacientes</button>
        </div>

      </form>

      
      </div>
    </div>
</template>





<style scoped>
/* Fondo y contenedor general */
.pagina-fondo {
  background-color: #072b4f;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

.contenedor-tarjeta {
  background: rgb(95, 93, 104);
  padding: 2rem;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.1);
  width: 100%;
  max-width: 600px;
}

.titulo {
  text-align: center;
  color: #ffffff;
  margin-bottom: 2rem;
}


.fila-formulario {
  display: grid;
  grid-template-columns: 1fr 2fr;
  align-items: center;
  margin-bottom: 1.2rem;
  gap: 10px;
}

label {
  font-weight: 600;
  color: #ffffff;
}

input, select {
  padding: 10px;
  border: 1px solid #053568;
  border-radius: 6px;
  font-size: 1rem;
}

input:focus, select:focus {
  outline: none;
  border-color: #000000; 
  box-shadow: 0 0 0 3px rgba(18, 27, 23, 0.1);
}

.acciones {
  display: flex;
  gap: 10px;
  justify-content: flex-end;
  margin-top: 1.5rem;
}

.btn-primario {
  background-color: #092742;
  color: white;
  border-color: aliceblue;
  padding: 12px 20px;
  border-radius: 6px;
  cursor: pointer;
  font-weight: bold;
}

.btn-primario:hover { background-color: #6a28d4; }

.btn-secundario {
  background-color: #718096;
  color: white;
  border-color: aliceblue;
  padding: 12px 20px;
  border-radius: 6px;
  cursor: pointer;
}

.mensaje-exito {
  margin-top: 20px;
  padding: 15px;
  background-color: #4f479f;
  color: #ffffff;
  border: 1px solid #b2f5ea;
  border-radius: 6px;
  text-align: center;
}
</style>
