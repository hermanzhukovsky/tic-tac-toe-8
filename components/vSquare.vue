<template>
	<button class="board__square" @click="$emit('test-click')" type="button">{{ squareItem.value }}</button>
</template>

<script>
export default {
	props: ["squareItem"],
	name: "vSquare",
}
</script>