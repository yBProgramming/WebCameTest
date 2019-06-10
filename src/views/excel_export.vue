<template>
  <v-container>
    <h1 style="text-align: center"> All User Lists </h1>
      
    <v-toolbar>
        <v-spacer></v-spacer>
        <v-btn color="success" @click="testFlutter()">Test Flutter</v-btn>
        <v-btn color="primary" @click="checkAndExports()"><v-icon>cloud_download</v-icon>  Export to excel</v-btn>
        <v-dialog
            v-model="dialog"
            width="350"
            >
            <!-- <v-btn
                slot="activator"
                color="primary"
                dark
            >
                Export to excel
            </v-btn> -->

            <v-card>
                <v-card-title
                class="headline"
                primary-title
                >
                Document export
                </v-card-title>

                <v-card-text>
                    Are you sure to export this document to excel?
                </v-card-text>

                <v-divider></v-divider>

                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="success"
                    flat
                    @click="handleDownload()"
                >
                    Export
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
    </v-toolbar>
      <v-data-table
            :headers="headers"
            :items="all_users"
            class="elevation-1"
        >
            <template slot="items" slot-scope="props">
            <td>{{ props.item.cusid }}</td>
            <td>{{ props.item.name }}</td>
            <td>{{ props.item.tel }}</td>
            <td>{{ props.item.type }}</td>
            <td class="text-xs-right">{{ props.item.status }}</td>
            <td class="text-xs-right">{{ props.item.create_date }}</td>
            </template>
        </v-data-table>
        <v-dialog
            v-model="error_dialog"
            width="350"
            >
            <v-card>
                <v-card-title
                class="headline"
                primary-title
                >
                Message
                </v-card-title>

                <v-card-text>
                    No data to export
                </v-card-text>

                <!-- <v-divider></v-divider> -->

                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="error"
                    flat
                    @click="error_dialog = false"
                >
                    OK
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>
  </v-container>
</template>

<script>
  import axios from 'axios'
  export default {
    data(){
        return {
            dialog: false,
            error_dialog: false,
            headers:[
                {
                    text: 'ID',
                    align: 'left',
                    sortable: true,
                    value: 'cusid'
                },
                { text: 'Full Name', value: 'name' },
                { text: 'Telephone', value: 'tel' },
                { text: 'Type', value: 'type' },
                { text: 'Status', value: 'status' },
                { text: 'Created', value: 'create_date' }
            ],
            all_users: [],
            downloadLoading: false
        }
    },
    mounted(){
        var me = this;
        // axios.get('http://10.0.10.72:8090/bcel/api/user/all')
        //     .then(function(result){
        //         me.all_users = result['data']['data'];
        //     })
    },
    methods: {
        testFlutter(){
            //alert(window['token']);
            console.log(`OK It's work as well from vuetify export file to excel page, , server: ${window['token']}`);
        },
        handleDownload() {
            this.downloadLoading = true
            import('@/vendor/Export2Excel').then(excel => {
                // console.log("OK It's work as well");
                const tHeader = ['ໄອດີ', 'ຊື່ ແລະ ນາມສະກຸນ', 'ເບີໂທ', 'ປະເພດ', 'ສະຖານະ', 'ວັນທີ່ແກ້ໄຂ', 'ວັນທີ່ສະໝັກ', 'ພະນັກງານ']
                const filterVal = ['cusid', 'name', 'tel', 'type', 'status', 'modify_date', 'create_date', 'staff']
                const list = this.all_users
                const data = this.formatJson(filterVal, list)
                excel.export_json_to_excel({
                    header: tHeader,
                    data,
                    filename: 'export-excel',
                    autoWidth: true,
                    bookType: 'xlsx'
                })
                this.downloadLoading = false
                this.dialog = false;
            })
        },
        formatJson(filterVal, jsonData) {
            return jsonData.map(v => filterVal.map(j => {
                if (j === 'timestamp') {
                return parseTime(v[j])
                } else {
                return v[j]
                }
            }))
        },
        checkAndExports(){
            if(this.all_users.length > 0){
                this.dialog = true;
            } else {
                this.error_dialog = true;
            }
        }
    }
  }
</script>
