<template>
  <div id="app">
		<div class="overlay" @click="closeAll"></div>
		<div class="content">
			<b-container fluid>
				<b-row class="my-1">
						<template v-for="book in RefBooks" >
							<b-col sm="3" v-bind:key="book.id">
								<b-form-input
										v-model="book.activeSelectItem"
										@focus="changeOptionsList(book.id)"
										placeholder="Товар прибыли"
										readonly></b-form-input>
								<RefBook :index="book.id"
													:options="book.options"
													@changeOptionsList="changeOptionsList"
													@changeItem="changeItem"
													:isSelectVisible="book.isSelectVisible"
													:selectHeader="book.selectHeader"/>
							</b-col>
						</template>
				</b-row>
			</b-container>
		</div>
  </div>
</template>

<script>
import RefBook from './components/RefBook.vue'

export default {
  name: 'App',
  components: {
		RefBook
  },
	data() {
		return {
			text: '',
			RefBooks: [
				{
					id: 0,
					activeSelectItem: 'Товар прибыл',
					isSelectVisible: false,
					selectHeader: 'Статус',
					options: [
						{
							"code": 0,
							"description": "Формируется"
						},
						{
							"code": 10,
							"description": "Товар прибыл"
						},
						{
							"code": 20,
							"description": "Товар прибыл (срочная поставка)"
						},
						{
							"code": 30,
							"description": "Оформление ДТ"
						},
						{
							"code": 40,
							"description": "ДТ выпущена"
						},
						{
							"code": 50,
							"description": "Поставка закрыта"
						}
					],
				},
				{
					id: 1,
					isSelectVisible: false,
					activeSelectItem: 'Импорт',
					selectHeader: 'Режим',
					options: [
						{
							"id": 1,
							"description": "Импорт"
						},
						{
							"id": 2,
							"description": "Экспорт"
						}
					],
				}
			],
		}
	},
	methods: {
		// метод открытия/закрытия справочника
		changeOptionsList: function (index) {
			this.RefBooks[index].isSelectVisible = !this.RefBooks[index].isSelectVisible;
		},
		// метод закрытия справочника по клику на overlay
		closeAll: function () {
			for(let i = 0; i < this.RefBooks.length; i++) {
				this.RefBooks[i].isSelectVisible = false;
			}
		},
		// метод для изменения значения поля input, выбор активного селект
		changeItem: function (index, name) {
			this.RefBooks[index].activeSelectItem = name;
		}
	}
}
</script>
