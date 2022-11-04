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
        desserts: [],
           editedItem: {
        name: '',
        description: '',
        changedFrom: '',
        changedTo: '',

      },


      }
    },
      // const fs = require("fs");
      //  this.desserts = fs.readFileSync("array.json","utf-8");
    created() {

      this.initialize()
    },

    methods: {

         close () {
        this.dialog = false
      },
      save () {

        this.desserts.push(this.editedItem)

        this.close()
      },
      initialize() {
        this.desserts = [
          {
            name: 'Noticeboard',
            description: '-> My team: \n' +
                '  Attendance & leave icon changed into finger print',
            changedFrom: 'mdi-calendar-check-outline',
            changedTo: 'mdi-fingerprint',

          },
          {
            name: 'Noticeboard',
            description: '-> My team: \n' +
                '  Subheading changed',
            changedFrom: 'Recent Information',
            changedTo: 'My Team\'s Attendance & Leave',

          },
          {
            name: 'Noticeboard',
            description: '-> Task Status: \n' +
                ' Task Status icon changed',
            changedFrom: 'mdi-calendar-check-outline ',
            changedTo: 'mdi-format-list-checks',

          },
          {
            name: 'Noticeboard',
            description: ' -> Task Status: \n' +
                ' Inside Task Detail of Task Status Task Comments changed ',
            changedFrom: 'mdi-calendar-check-outline',
            changedTo: 'mdi-message-processing-outline',

          },
          {
            name: 'Noticeboard',
            description: ' -> Task Status: \n' +
                ' Inside Task Detail of Task Status Task Reminder icon changed ',
            changedFrom: 'mdi-calendar-check-outline',
            changedTo: 'mdi-calendar-month-outline',

          },
          {
            name: 'Noticeboard',
            description: ' -> Task Status: \n' +
                ' Inside Task Reminder of Task Detail Reminder At icon changed ',
            changedFrom: 'mdi-flag-outline',
            changedTo: 'mdi-account',

          },
          {
            name: 'Tasks',
            description: ' -> Task Feedback: \n' +
                ' Inside Task Feedback of Task Approvals Reminder At icon changed ',
            changedFrom: 'mdi-checkbox-marked-outline',
            changedTo: 'mdi-message-processing-outline',

          },
          {
            name: 'Tasks',
            description: ' -> Task Feedback: \n' +
                ' Inside Task Feedback of Task Approvals Subheading changed ',
            changedFrom: 'Refer to the following information for your task approvals.',
            changedTo: 'The table below contains list of your task feedback',

          },
          {
            name: 'Tasks',
            description: ' -> Task Feedback: \n' +
                ' Title changed ',
            changedFrom: 'Task Approvals',
            changedTo: 'Task Feedback',

          },
          {
            name: 'Tasks',
            description: ' -> Worklog: Subheading changed',
            changedFrom: 'Refer the following information for worklog.',
            changedTo: 'The table below contains list of your worklog.',

          },
          {
            name: 'Tasks',
            description: ' -> Worklog: Inside of Create Work Log form, icon changed of Project Name field',
            changedFrom: 'mdi-account-multiple',
            changedTo: 'mdi-briefcase-outline',

          },
          {
            name: 'Tasks',
            description: ' -> Worklog: Inside of Create Work Log form, icon changed of Activity Name field',
            changedFrom: 'mdi-account-multiple',
            changedTo: 'mdi-file-table-box-multiple-outline',

          },
          {
            name: 'Tasks',
            description: ' -> Worklog: Inside of Create Work Log form, icon changed of Core Task field',
            changedFrom: 'mdi-account-multiple ',
            changedTo: 'mdi-format-list-checks',

          },
          {
            name: 'Tasks',
            description: ' -> Worklog: Inside of Create Work Log form, icon changed of Task Name field',
            changedFrom: 'mdi-account-multiple ',
            changedTo: 'mdi-format-list-checks',

          },
          {
            name: 'Tasks',
            description: ' -> Reports : Icon changed of Task Efficiency which is inside of Efficiency',
            changedFrom: 'mdi-file-chart-outline',
            changedTo: 'mdi-chart-box',

          },
          {
            name: 'Tasks',
            description: ' -> Reports: Icon changed of Payload which is inside of Payload',
            changedFrom: 'mdi-format-list-bulleted ',
            changedTo: 'mdi-clipboard-text',

          },
          {
            name: 'Work logs',
            description: ' -> Leaderboard: Icon changed of Worklog Leaderboard ',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-account-circle-outline',

          },
          {
            name: 'Work logs',
            description: ' -> Leaderboard: Icon changed of Log Efficiency',
            changedFrom: 'mdi-file-document-outline ',
            changedTo: 'mdi-format-list-checkbox',

          },
          {
            name: 'Attendance',
            description: ' -> Request: Icon changed of Pre Approval Overtime Request which is inside of pre approval',
            changedFrom: 'mdi-file-document ',
            changedTo: 'mdi-send-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Request: Icon changed of Credit Hour Request  which is inside of Credit Hour Request ',
            changedFrom: 'mdi-file-document ',
            changedTo: 'mdi-circle-slice-5',

          },
          {
            name: 'Attendance',
            description: ' -> Request: Icon changed of Timesheet Requests which is inside of Timesheet Requests ',
            changedFrom: 'mdi-file-document ',
            changedTo: 'mdi-calendar-check-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Request: Inside of Timesheet Requests click action icon and go to Proceed button - The icon of Request for Approval is changed',
            changedFrom: 'mdi-calendar-month-outline',
            changedTo: 'mdi-send-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Request: Inside of Timesheet Requests click action icon and go to Regenerate button - The icon of Confirm Timesheet Regenerationis changed',
            changedFrom: 'mdi-calendar-month-outline',
            changedTo: 'mdi-sync',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Break In / Break Out Report which is inside of Break In / Break Out',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-swap-horizontal',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Attendance Entry Report which is inside of Attendance Entries',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-calendar-edit',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Overtime Claim History which is inside of Overtime',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-alarm-plus',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Individual Daily Attendance which is inside of Individual Daily Attendance',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-fingerprint',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Monthly Attendance which is inside of Monthly Attendance',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-calendar-clock',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Attendance Irregularities which is inside of Irregularities',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-clock-alert-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Credit Hour Delete Request History ',
            changedFrom: 'mdi-send',
            changedTo: 'mdi-delete-sweep-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Icon changed of Travel Attendance Delete History ',
            changedFrom: 'mdi-train-car',
            changedTo: 'mdi-trash-can-outline',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Subheading changed of Break In / Break Out Report which is inside of Break In / Break Out Report  ',
            changedFrom: 'The table below contains list of break in / break out information',
            changedTo: 'The list below contains list of break in / break out information',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Subheading changed of Individual Daily Attendance which is inside of Individual Daily Attendance',
            changedFrom: 'This page contains information about individual daily attendance.',
            changedTo: 'This list contains information about individual daily attendance.',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Subheading changed of Monthly Attendance which is inside of Monthly Attendance ',
            changedFrom: 'This page contains information about Monthly attendance.',
            changedTo: 'This list contains information about Monthly attendance.',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Subheading changed of Credit Hour Delete Request History which is inside of Credit Hour Delete Request History  ',
            changedFrom: 'Credit hour delete request history by you.',
            changedTo: 'This list below contains information about Credit hour delete request history by you.',

          },
          {
            name: 'Attendance',
            description: ' -> Reports: Subheading changed of Attendance Penalty which is inside of Penalty ',
            changedFrom: 'Here you can view the attendance penalty',
            changedTo: 'This list below contains information about attendance penalty.',

          },
          {
            name: 'Leave',
            description: ' -> Leave Encashment: Icon changed of  Leave Encashment Report which is inside of Leave Encashment ',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-cash',

          },
          {
            name: 'Leave',
            description: ' -> Leave History : Icon changed of Leave Request From Rajesh Shrestha  which is inside of action eye icon ',
            changedFrom: 'mdi-calendar-remove-outline',
            changedTo: 'mdi-send-outline',

          },
          {
            name: 'Payroll',
            description: ' -> Payslip and Tax: Icon changed of Payslip and Tax which is inside of list',
            changedFrom: 'mdi-cash',
            changedTo: 'mdi-cash-100',

          },
          {
            name: 'Payroll',
            description: ' -> Unit of Work Done: Icon changed of Unit of Work Done which is inside of Unit of Work Done',
            changedFrom: 'mdi-send',
            changedTo: 'mdi-cash',

          },
          {
            name: 'Payroll',
            description: ' -> Rebate: Icon changed of Rebate Requests which is inside of Rebate',
            changedFrom: 'mdi-file-document-outline',
            changedTo: 'mdi-cash-multiple',

          },
          {
            name: 'Payroll',
            description: ' -> Payslip and Tax : Subheading changed of Payslip and Tax which is inside List',
            changedFrom: 'Below is the list of generated payroll.',
            changedTo: 'The list below is the list of generated payroll.',

          },
          {
            name: 'Payroll',
            description: ' -> Unit of Work Done : Inside request button :- Icon of Request unit of work done is changed',
            changedFrom: 'mdi-plus-box-outline',
            changedTo: 'mdi-send-outline',

          },
          {
            name: 'Payroll',
            description: ' -> Advance Salary : Inside Request Advance button :- Icon of Request Advance is changed',
            changedFrom: 'mdi-currency-usd',
            changedTo: 'mdi-send-outline',

          },

        ]

      }
    }
  }

</script>
<style scoped>

.v-data-table .v-data-table__wrapper thead th {
      font-size: 50px !important;
  font-weight: 800;

 }
</style>