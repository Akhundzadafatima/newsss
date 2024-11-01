<template>
  <h1>Home Page</h1>
  <div class="containerr">
    <h3>Book Mark List</h3>
    <button class="addBtn" @click="$router.push({ name: 'NewBookMark' })">
      + Yeni element əlavə et
    </button>
    <table id="customers">
      <tr>
        <th>#</th>
        <th>Başlıq</th>
        <th>URL</th>
        <th>Açıqlama</th>
        <th>Sil</th>
      </tr>
      <tr v-for="bookmark in bookmarkList" :key="bookmark.id">
        <td>{{ bookmark.id }}</td>
        <td>{{ bookmark.title }}</td>
        <td>
          <a :href="bookmark.url">{{ bookmark.url }}</a>
        </td>
        <td>{{ bookmark.description }}</td>
        <td>
          <button class="deleteBtn" @click="deleteBookmark(bookmark)">Sil</button>
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      bookmarkList: [],
    };
  },
  created() {
    this.$appAxios.get("/bookmarks").then((bookmarks_list_response) => {
      // console.log(bookmarks_list_response);
      this.bookmarkList = bookmarks_list_response.data || [];
    });
  },
  methods:{
    deleteBookmark(bookmark){
      this.$appAxios.delete(`/bookmarks/${bookmark.id}`).then(delete_response=>{
if(delete_response.status==200){
  this.bookmarkList=this.bookmarkList.filter(b=>b.id !== bookmark.id)
}
      })


      console.log("bookmark:", bookmark);
      
    },
  }
};
</script>
