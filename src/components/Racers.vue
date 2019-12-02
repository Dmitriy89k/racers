<template>
    <div>
        <el-table
                :data="racersDisplay"
                style="width: 100%"
        >
            <el-table-column
                    prop="familyName"
                    label="Family name"
                    width="180"
            />
            <el-table-column
                    prop="givenName"
                    label="First name"
                    width="180"
            />
            <el-table-column
                    prop="dateOfBirth"
                    label="Date of birth"
                    width="180"
            />
            <el-table-column label="biography">
                <template slot-scope="scope">
                    <a v-bind:href= getUrl(scope.$index)>Wiki</a>
                </template>
<!--                <template slot-scope="{row}">-->
<!--                    <a :href=row>Wiki</a>-->
<!--                </template>-->
            </el-table-column>
        </el-table>
        <div class="block">
            <el-pagination
                    layout="prev, pager, next"
                    :total="170"
                    @current-change="changePage"
            />
        </div>
    </div>
</template>

<script>
 import axios from 'axios';

 export default {
  name: 'Racers',

    data: () => ({
      racersDisplay: [],
      racers: []
     }),

    mounted(){
          this.changePage(1);
        },

     methods: {
      getUrl(id){
         return this.racersDisplay[id].url
      },
       changePage(pageNumber){
         let offset = 50 * pageNumber - 1;
           this.loadRacers(offset)
       },
         loadRacers(offset){
             axios.get(`http://ergast.com/api/f1/drivers.json?limit=50&offset=${offset}`)
                 .then(response => {
                     this.racersDisplay = response.data.MRData.DriverTable.Drivers
                 })
         }
     },
  }
</script>
