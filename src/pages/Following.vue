<template>
  <q-page>
  <div id="q-app">
    <div class="q-pa-md">
      <q-table
        title="Treats"
        :data="data"
        :columns="columns"
        row-key="name"
        selection="multiple"
        :selected.sync="selected"
        :filter="filter"
      >
        <template v-slot:top>
          <q-btn dense color="secondary" label="Add Row" @click="show_dialog = true" no-caps></q-btn>
          <div class="q-pa-sm q-gutter-sm">
            <q-dialog v-model="show_dialog">
              <q-card>
                <q-card-section>
                  <div class="text-h6">Add new item!</div>
                </q-card-section>
                <q-card-section>
                  <div class="row">
                    <q-input v-model="editedItem.name" :class="[editedItem.name.length < 2 ? 'red' : 'green']" label="Dessert Name"></q-input>
                    <q-input v-model="editedItem.calories" label="Calories"></q-input>
                    <q-input v-model="editedItem.fat" label="Fat"></q-input>
                    <q-input v-model="editedItem.protein" label="Protein"></q-input>
                  </div>
                </q-card-section>
                <q-card-actions align="right">
                  <q-btn flat label="OK" v-bind:disabled="editedItem.name.length < 2" color="primary" v-close-popup @click="addRow" ></q-btn>
                </q-card-actions>
              </q-card>
            </q-dialog>
          </div>
        </template>

        <template v-slot:body-cell-action="props">
          <q-td :props="props">
            <q-btn color="blue" label="Update" @click="editItem(props.row)" size=sm no-caps></q-btn>
            <q-btn color="red" label="Delete"  @click="deleteItem(props.row)" size=sm no-caps></q-btn>
          </q-td>
        </template>
      </q-table>

      <q-btn
        style="position: absolute; left: 150px; top: 20px;"
        color="red"
        icon-right="delete_forever"
        no-caps
        @click="deleteSelected"
      />
    </div>
    <q-input style="position: absolute; top: 15px; left: 290px;" v-model="filter" placeholder="Search">
      <template v-slot:append>
        <q-icon name="search" />
      </template>
    </q-input>
  </div>
  </q-page>
</template>

<script>
    export default {
        data() {
            return {
                filter: '',
                show_dialog: false,
                editedIndex: -1,
                editedItem: {
                    name: "",
                    calories: 0,
                    fat: 0,
                    protein: 0,
                },
                defaultItem: {
                    name: "",
                    calories: 0,
                    fat: 0,
                    protein: 0,
                },
                selected: [],
                columns: [
                    {
                        name: 'desc',
                        required: true,
                        label: 'Name',
                        align: 'left',
                        field: row => row.name,
                        format: val => `${val}`,
                        sortable: true
                    },
                    {name: 'Surname', align: 'center', label: 'Surname', field: 'calories', sortable: true},
                    {name: 'MobileNumber', label: 'MobileNumber', field: 'fat', sortable: true},
                    {name: 'Position', label: 'Position', field: 'protein'},
                    {name: 'Status', label: 'Status', field: 'Status'},
                    {name: 'Password', label: 'Password', field: 'Password'},
                    {name: 'action', label: 'Action', field: 'action'}
                ],
                data: [
                    {
                        name: 'John',
                        calories: 'Doe',
                        fat: '+99511111111',
                        protein: 'Developer',
                        Status:'Active',
                        Password:'test123'
                    },
                    {
                        name: 'Jane',
                        calories: 'Doe',
                        fat: '+99522222222',
                        protein: 'HR',
                        Status:'Active',
                        Password:'54321'
                    },
                    {
                        name: 'George',
                        calories: 'Wine',
                        fat: '+99533333333',
                        protein: 'Security',
                        Status:'Active',
                        Password:'789456'
                    },
                    {
                        name: 'Piter',
                        calories: 'Parker',
                        fat: '+99555555555',
                        protein: 'SpiderMane',
                        Status:'Active',
                        Password:'Spiderman'
                    },
                ]
            }
        },
        methods: {
            deleteSelected() {
                let self = this;
                confirm("Are you sure you want to delete this items?") &&
                this.selected.filter(function (item) {
                    self.data.splice(self.data.indexOf(item), 1);
                    return item;
                });
                this.selected = [];
            },
            addRow() {
                if (this.editedIndex > -1) {
                    Object.assign(this.data[this.editedIndex], this.editedItem);
                } else {
                    this.data.push(this.editedItem);
                }
                this.close()
            },
            deleteItem(item) {
                const index = this.data.indexOf(item);
                confirm("Are you sure you want to delete this item?") &&
                this.data.splice(index, 1);
            },
            editItem(item) {
                this.editedIndex = this.data.indexOf(item);
                this.editedItem = Object.assign({}, item);
                this.show_dialog = true;

            },
            close () {
                this.show_dialog = false
                setTimeout(() => {
                    this.editedItem = Object.assign({}, this.defaultItem)
                    this.editedIndex = -1
                }, 300)
            }
        },
    }
</script>

<style scoped>
  .red {
    border: 2px solid red;
  }
  .green {
    border: 2px solid green;
  }

</style>

a
