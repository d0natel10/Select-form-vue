<template>
  <div class="body">
    <div class="form-container">
      <h1>Select Form Vue</h1>
  
      <label for="city">Город:</label>
      <select v-model="selectedCity" @change="updateDeparts" class="styled-select">
        <option v-for="city in cities" :key="city" :value="city">{{ city }}</option>
      </select>
  
      <label for="depart">Цех:</label>
      <select v-model="selectedDepart" @change="updateEmployees" class="styled-select">
        <option v-for="depart in departs" :key="depart" :value="depart">{{ depart }}</option>
      </select>
  
      <label for="employee">Сотрудник:</label>
      <select v-model="selectedEmployee" @change="updateTeams" class="styled-select">
        <option v-for="employee in employees" :key="employee" :value="employee">{{ employee }}</option>
      </select>
  
      <label for="team">Бригада:</label>
      <select v-model="selectedTeam" class="styled-select">
        <option v-for="team in teams" :key="team" :value="team">{{ team }}</option>
      </select>
  
      <label for="shift">Смена:</label>
      <select v-model="selectedShift" class="styled-select">
        <option v-for="shift in shifts" :key="shift" :value="shift">{{ shift }}</option>
      </select>
  
      <div class="button-container">
        <button @click="saveToCookies" class="save-btn">Сохранить</button>
      </div>
    </div>
  </div>
  </template>
  
  <script>
  import { ref, watch } from 'vue';
  
  export default {
    setup() {
      const cities = ['Москва', 'Санкт-Петербург', 'Казань'];
      const departs = ref([]);
      const employees = ref([]);
      const teams = ['Бригада 1', 'Бригада 2', 'Бригада 3'];
      const shifts = ['1 смена', '2 смена', '3 смена'];
  
      const selectedCity = ref('');
      const selectedDepart = ref('');
      const selectedEmployee = ref('');
      const selectedTeam = ref('');
      const selectedShift = ref('');
  
      function updateDeparts() {
        if (selectedCity.value === 'Москва') {
          departs.value = ['Основной цех', 'Побочный цех'];
        } else if (selectedCity.value === 'Санкт-Петербург') {
          departs.value = ['Основной цех', 'Заготовительный цех', 'Сборочный цех'];
        } else {
          departs.value = ['Обслуживающий цех'];
        }
  
        selectedDepart.value = '';
        selectedEmployee.value = '';
        selectedTeam.value = '';
      }
  
      function updateEmployees() {
        if (selectedDepart.value === 'Основной цех') {
          employees.value = ['Петров А.', 'Васильев Б.'];
        } else if (selectedDepart.value === 'Побочный цех') {
          employees.value = ['Иванов А.', 'Дрозд Е.'];
        } else {
          employees.value = ['Гущев К.', 'Ломов Н.'];
        }
  
        selectedEmployee.value = '';
        selectedTeam.value = '';
      }
  
      function updateTeams() {
        if (selectedEmployee.value === 'Перов А.') {
          teams.splice(0, teams.length, 'Бригада 1', 'Бригада 2');
        } else {
          teams.splice(0, teams.length, 'Бригада 1', 'Бригада 2', 'Бригада 3');
        }

        selectedTeam.value = '';
      }
  
      function saveToCookies() {
        document.cookie = `selectedCity=${JSON.stringify(selectedCity.value)}`;
        document.cookie = `selectedDepart=${JSON.stringify(selectedDepart.value)}`;
        document.cookie = `selectedEmployee=${JSON.stringify(selectedEmployee.value)}`;
        document.cookie = `selectedTeam=${JSON.stringify(selectedTeam.value)}`;
        document.cookie = `selectedShift=${JSON.stringify(selectedShift.value)}`;
  
        alert('Данные сохранены в cookie!');
      }
  
      watch(selectedCity, () => saveToCookies);
      watch(selectedDepart, () => saveToCookies);
      watch(selectedEmployee, () => saveToCookies);
      watch(selectedTeam, () => saveToCookies);
      watch(selectedShift, () => saveToCookies);
  
      return {
        cities,
        departs,
        employees,
        teams,
        shifts,
        selectedCity,
        selectedDepart,
        selectedEmployee,
        selectedTeam,
        selectedShift,
        updateDeparts,
        updateEmployees,
        updateTeams,
        saveToCookies
      };
    }
  };
  </script>