<template>
 <v-main>

<v-container>

<!--  <v-text-field-->
<!--        v-model="search"-->
<!--        append-icon="mdi-magnify"-->
<!--        label="Search"-->
<!--        single-line-->
<!--        hide-details-->
<!--      ></v-text-field>-->
  <v-data-table
    :headers="headers"
    :items="desserts"
    group-by="name"
    :items-per-page="10"
    class="elevation-1"
    show-group-by


  >

    <template v-slot:top>
      <v-toolbar
        flat
      >
    <v-toolbar-title>UI Correction Data Table</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
         <v-spacer></v-spacer>
        <v-dialog
          v-model="dialog"
          max-width="500px"
        >
          <template v-slot:activator="{ on, attrs }">
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              New Item
            </v-btn>
          </template>
          <v-card>
            <v-card-title>
              <span class="text-h5">{{  }}</span>
            </v-card-title>

            <v-card-text>
              <v-container>

                  <v-row

                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                      v-model="editedItem.name"
                      label="Module name"
                    ></v-text-field>
                  </v-row>
                  <v-row

                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field
                       v-model="editedItem.description"
                      label="Description"
                    ></v-text-field>
                  </v-row>
                  <v-row

                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field

                      label="Changed From"
                      v-model="editedItem.changedFrom"
                    ></v-text-field>
                  </v-row>
                  <v-row

                    cols="12"
                    sm="6"
                    md="4"
                  >
                    <v-text-field

                      label="Changed To"
                      v-model="editedItem.changedTo"
                    ></v-text-field>
                  </v-row>


              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="save"
              >
                Save
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </v-toolbar>

        </template>
   <template v-slot:[`item.changedFrom`]="{item}">
       <v-icon v-if="(item.changedFrom).startsWith('mdi-')">{{item.changedFrom}}</v-icon>
       <span v-else>{{item.changedFrom}}</span>
     </template>
    <template v-slot:[`item.changedTo`]="{item}">
       <v-icon v-if="(item.changedTo).startsWith('mdi-')">{{item.changedTo}}</v-icon>
       <span v-else>{{item.changedTo}}</span>
     </template>
    </v-data-table>

   </v-container>
</v-main>

</template>

<script>
import json from "../assets/array";

  export default {
    data() {
      return {
        dialog: false,
        search: '',
        headers: [
          {
            text: 'Module',
            align: 'start',
            value: 'name',


          },
          {text: 'Description', value: 'description', groupable: false,},
          {text: 'Changed From', value: 'changedFrom'},
          {text: 'Changed To', value: 'changedTo'},
        ],
        desserts: json.desserts,
        editedItem: {
        name: '',
        description: '',
        changedFrom: '',
        changedTo: '',

      },


      }
    },

    created() {


    },



    methods: {
      saveData(editedItem){
    const fs=require('fs')
    const jsonData=JSON.stringify(editedItem,null,2)
    fs.writeFile('../assets/array.json',jsonData)
  },

         close () {
        this.dialog = false
      },
      save () {
        this.saveData()
        // this.desserts.push(this.editedItem)

        this.close()
      },

    }
  }

</script>
<style scoped>

.v-data-table .v-data-table__wrapper thead th {
      font-size: 50px !important;
  font-weight: 800;

 }
</style>