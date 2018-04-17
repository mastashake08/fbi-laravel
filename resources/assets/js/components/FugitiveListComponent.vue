<template>
    <div class="container">
        <div class="row justify-content-center">
            <div class="col-md-8">
                <div class="card card-default">
                    <div class="card-header">FBI Wanted Fugitives</div>

                    <div class="card-body table-responsive">

                      <table class="table">
                        <thead>
                          <tr>
                            <th>Picture</th>
                            <th>Name</th>
                            <th>Field Office</th>
                            <th>Description</th>
                            <th>Caution</th>
                          </tr>
                        </thead>
                        <tbody>
                          <tr v-for="fugitive in fugitivesObject.items">
                            <td><img :src="fugitive.images[0].thumb" class="img img-responsive img-rounded"/></td>
                            <td>{{fugitive.title}}</td>
                            <td>{{fugitive.field_office}}</td>
                            <td><div v-html="fugitive.details"></div></td>
                            <td><div v-html="fugitive.caution"></div></td>
                          </tr>
                        </tbody>
                      </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        mounted() {
            console.log('Component mounted.')
        },
        created(){
          var that = this;
          axios.get(this.url).then(function(data){
            that.fugitivesObject = data.data;
          });
        },
        data(){
          return {
            url: '/api/fugitive',
            fugitivesObject : {}
          }
        },
        methods:{
          getPage:function(page){
              var that = this;
              axios.get(this.url+'list?page='+page).then(function(data){
                that.fugitivesObject = data.data;
              });
          }
        }
    }
</script>
