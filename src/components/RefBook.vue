<template>
  <div class="refBook" v-show="isSelectVisible">
		<div class="refBook-select">
			<div class="refBook-option refBook-option-head" @click="changeList">{{ selectHeader }} <b-icon icon="x" font-scale="1.5" style="color: #495057;"></b-icon> </div>
			<div class="refBook-option"  v-for="item in options" :key="item.id" @click="changeOptionsItem(item.description)">{{ item.description }}</div>
		</div>
  </div>
</template>

<script>
export default {
  name: 'RefBook',
	props: {
		options: { type: Array },
		selectHeader: { type: String },
		isSelectVisible: { type: Boolean },
		index: { type: Number }
	},
	data() {
		return {
			selectedUsers:[]
		}
	},
	methods:  {
		// // open and close All statuses list
		changeList: function () {
			this.$emit('changeOptionsList', this.index)
		},
		// change chosen list item in select
		changeOptionsItem: function (item) {
			this.$emit('changeItem', this.index, item);
			this.$emit('changeOptionsList', this.index);
		},
	},
}
</script>

