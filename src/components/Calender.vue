<template>
  <div id="calender">
    <!--display table starts -->
       <div class="card">
          <div class="row card_inner">
             <div class="col-md-3"></div>
             <div class="col-md-3 form-group">
                  <select class= "form-control"  v-model = "cur_month"  @change = "changeMonth()">          
                       <option v-for = "(month,index) in months" :value = "month" :key = "index"> {{month}} </option>
                  </select>
             </div>
             <div class="col-md-3 form-group">
                <select class="form-control"  v-model= "cur_year"  @change= "changeYear()">
                    <option v-for= "(year,index) in years" :value= "year" :key= "index">{{year}}</option>
                </select>
             </div>
             <div class="col-md-12 ">  
                              <table class="table display table-bordered">
                                 <thead style=" position: sticky;">
                                    <tr>
                                       <th>Sun</th>
                                       <th>Mon</th>
                                       <th>Tue</th>
                                       <th>Wed</th>
                                       <th>Thu</th>
                                       <th>Fri</th>
                                       <th>sat</th>
                                    </tr>
                                 </thead>
                                 <tbody>
                                   
                                    <tr  v-for='(days,index) in total_days' :key='index'>
                                       <td v-for='(day,index) in days' :key='index'>{{ day}}</td>
                                        <!-- <td v-for='(day,index) in total_days' :key='index'>{{ day }}</td> -->
                                       <!-- <td>{{day}}</td> -->
                                    </tr>
                                 </tbody>
                              </table>

              </div>
            </div>
          </div> 
     <!--display table ends -->
    <!-- body ends -->               
  </div>
</template>

<script>
export default {
  data(){
    return{
        total_days:[],
        cur_month:'',
        cur_year:'',
        months:["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"],
        years:[],
    }
  },
  methods:{
    changeMonth(){
        this.total_days = [];
        let m = this.months.findIndex((el)=>el==(this.cur_month)); 
        let y = this.cur_year;
        this.displayDays(y,m);
    },
    changeYear(){
        this.total_days = [];
        let m = this.months.findIndex((el)=>el==(this.cur_month));
        let y = this.cur_year;
        this.displayDays(y,m);
    },
    setMonthYear(){
        let current_month = new Date().toLocaleString('default', { month: 'short' });
        this.cur_month = current_month;
        let start_year = 2010;
        let end_year = 2020;

        for(let i=start_year;i<=end_year;i++){
           this.years.push(i);
        }
        let current_year =  new Date().getFullYear();
        this.cur_year = current_year;
        console.log(this.cur_year);
    },

    getDates(){
        let date = new Date(), y = date.getFullYear(), m = date.getMonth();
        this.displayDays(y,m);
    },

    displayDays(y,m){
        var month_days = [];
        let firstDay = new Date(y, m, 1).getDay();
        let lastDay = new Date(y, m + 1, 0).getDay(); 
           
      //starting empty days   
        for(let i=0;i<firstDay;i++){
            month_days.push(undefined);
        }
      // month days
        let num_days =  new Date(y, m+1, 0).getDate();
        for(let i=1;i<=num_days;i++){
            month_days.push(i);
        }

      //ending empty days 
        for(let i=lastDay;i<7;i++){
           month_days.push(undefined);
        }

      //format month days
        for(let i=0;i<=(month_days.length);i++){
            let sub_days = [];
            sub_days =  month_days.splice(0,7);
            this.total_days.push(sub_days);
        }

    },

  },
  mounted() {
       this.getDates();
       this.setMonthYear();
  },
}
</script>
<style scoped>
   .table th,td{
      text-align: center;
   }
   .table th{
      padding:14px; 
   }
   .table td{
      padding:30px; 
      font-size: 20px;
   }
   .table td:hover{
      background-color: #eee;
   }
   .table-bordered td,th {
      border: 4px solid #dee2e6d1;
  }
  .table {
    border-radius: 1px;
    border-collapse: 0px;;
  }
</style>

