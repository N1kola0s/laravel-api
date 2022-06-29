<template>
  <div>
    <work-in-progress></work-in-progress>

    <section class="posts">
      <div class="container">
        <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 my-5">
          <div class="col" v-for="post in postsResponse.data" :key="post.id">
            <div class="product card">
              <img :src="'storage' + post.cover_image" :alt="post.title" />

              <div class="card-body">
                <h3>{{ post.title }}</h3>
                <p>{{ post.content }}</p>
              </div>
              <!-- .card-body -->

              <div class="card-footer">
                <div class="col">
                  <span>
                    <strong> Author: </strong>

                    Io me e me stesso
                  </span>
                </div>
                <!-- .col -->

                <div class="col">
                  <span v-if="post.category">
                    <strong> Category: </strong>

                    {{ post.category.name }}
                  </span>

                  <div class="tags" v-if="post.tags.length > 0">
                    <strong> Tags: </strong>

                    <span v-for="tag in post.tags" :key="tag.id">
                      <a href="#">{{ tag.name }}</a> - 
                    </span>
                  </div>
                  <!-- /.tags -->
                </div>
                <!-- /.col -->
              </div>
              <!-- /.card-footer -->
            </div>
            <!-- /.product  -->
          </div>
          <!-- /.col -->
        </div>
        <!-- /.row -->
      </div>
      <!-- /.container -->
    </section>
    <!-- /.posts -->
  </div>
</template>

<script>
import WorkInProgress from "../components/WorkInProgress";
export default {
  name: "App",
  components: {
    WorkInProgress,
  },
  data() {
    return {
      posts: "",
      postsResponse: "",
    };
  },
  methods: {
    getAllPosts() {
      axios
        .get("/api/posts")
        .then((response) => {
          /* console.log(response.data.data); */
          this.posts = response.data.data;
          this.postsResponse = response.data;
        })
        .catch((e) => {
          console.error(e);
        });
    },
  },
  mounted() {
    /* console.log('mounted'); */
    this.getAllPosts();
  },
};
</script>
