<template>
<v-card flat>
    <v-card-text>
      <v-container fluid>
        <v-row>
          <v-rating
            v-model="rating"
            background-color="purple lighten-3"
            large
          ></v-rating>
        </v-row>
        <v-row class="mt-5">
            <v-text-field
            v-model="title"
            placeholder="제목을 입력하세요"
            outlined
          ></v-text-field>
        </v-row>
        <v-row>
  <v-file-input
    v-model="file"
    label="File input"
    outlined
    dense
  ></v-file-input>
        </v-row>
          <v-row>
              <v-textarea
              v-model="comment"
              label="내용을 입력하세요"
              outlined
            >
            </v-textarea>
          </v-row>
      </v-container>
      <v-card-actions>
        <v-btn
          text>
          Cancel
        </v-btn>
        <v-spacer></v-spacer>
        
        <v-btn
          :disabled="!formIsValid"
          text
          color="primary"
          @click="submit">
          Add
        </v-btn>
        
      </v-card-actions>
      </v-card-text>
  </v-card>  
</template>

<script>
export default {
data(){
 return{
     rating: this.rating,
     title: this.title,
     file: [],
     comment: this.comment
 }   
},
methods:{
    submit(){
      const id = Number(this.$route.params.contentId);
      var formData = new FormData();
      formData.append('rating',this.rating);
      formData.append('title',this.title);
      formData.append('content',this.comment);
      formData.append('attachFile', this.file);
      formData.append('productId', id)
      this.$http
      .post('/api/dashboard/orders/products', formData,{
       withCredentials:true
      })
     .then(res => {
      console.log(res);
      })
     .catch(err => {
       console.log(err);
    });
    }
},
computed: {
    formIsValid(){
      return (
        this.title &&
        this.comment
      )},
}
}
</script>

<style>

</style>