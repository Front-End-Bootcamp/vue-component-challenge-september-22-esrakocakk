<script setup>

import DATA from '@/assets/data/data.json';
import { onMounted, ref } from 'vue';

const data = ref([]);

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


onMounted(async () =>{
	data.value = await filterByGroups();
})

</script>

<template>
<div>

</div>
</template>

<style scoped>

</style>