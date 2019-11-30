<template>
    <div>
      <el-table
            :data="racersDisplay"
            style="width: 100%">
        <el-table-column
                prop="familyName"
                label="Family name"
                width="180">
        </el-table-column>
        <el-table-column
                prop="givenName"
                label="First name"
                width="180">
        </el-table-column>
        <el-table-column
                prop="dateOfBirth"
                label="Date of birth"
                width="180">
        </el-table-column>
        <el-table-column
                 label="biography">
            <template slot-scope="scope">
                <a v-bind:href= getUrl(scope.$index)>Wiki</a>
            </template>
        </el-table-column>
      </el-table>
        <div class="block">
            <el-pagination
                    layout="prev, pager, next"
                    :total="170"
                    @current-change="(event) => {changePage(event, id)}"
            >
            </el-pagination>
        </div>
    </div>
</template>

<script>
 import axios from 'axios';

 export default {
  name: 'Racers',

    data: () => ({
      racersDisplay: [],
      id: null,
      racers: []
     }),

    mounted(){
      axios.get(`http://ergast.com/api/f1/drivers.json?limit=847`)
        .then(response => {
          this.racers = response.data.MRData.DriverTable.Drivers
          this.changePage(1);
        })


    },
     methods: {
      getUrl(id){
         return this.racers[id].url
      },
       changePage(id){
         this.racersDisplay = this.racers.slice(id*50-50, id*50)
        }
     },

  }
</script>
