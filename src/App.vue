<script setup>
import BootcampLogo from "./assets/svg/BootcampLogo.vue"
import HelloWorld from './components/HelloWorld.vue'

//json dosyası import edildi.
import DATA from '@/assets/data/data.json';
import { onMounted, ref } from 'vue';


const data = ref([]);

//json dosyası içindeki veriler grupsal olarak ayrıldı.
function getGroupNames(data){
	const groupNames = data.map(person => person.group);
	const uniqueNames = [...new Set(groupNames)];
	return uniqueNames;
}
function filterByGroups(data){
	const groups = data.reduce((currentData, person) => {
		if(!currentData[person.group]){
			currentData[person.group] = []
		}

		return currentData;
	}, {});


Object.keys(groups).forEach(group => {
	const students = data.filter(person => person.group == group);
	groups[group] = students;
})

return groups
}

const names = getGroupNames(DATA);
console.log(names);

const groups = filterByGroups(DATA);
console.log(groups);
</script>

<template>

	<div>
		{{names}}
		<br>
	</div>
</template>

<style scoped>
.logo {
	height: 6em;
	padding: 1.5em;
	will-change: filter;
}

.logo:hover {
	filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
	filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
