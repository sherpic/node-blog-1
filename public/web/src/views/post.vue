<template>
    <div>
        <PathNav :paths="paths"></PathNav>

        <Post :post="post"></Post>

        <p class="comment-list-tip">华丽分割线</p>

        <CommentBox url="/ajax/post/comment/add" :post_id="post._id"></CommentBox>

        <CommentList :comments="comments" :post_id="post._id"></CommentList>

    </div>

</template>

<script>

    import Post from '../components/Post.vue'
    import PathNav from '../components/PathNav.vue'
    import CommentBox from '../components/CommentBox.vue'
    import CommentList from '../components/CommentList.vue'

    export default{

        components: {
            Post,
            PathNav,
            CommentBox,
            CommentList,
        },
        data () {
            return {
                comment_nums: []
            }
        },
        beforeMount () {
            this.fetch(this.$store)
        },
        methods: {
            fetch(store) {
                return store.dispatch('loadPost', this.$route.params.id)
            }
        },
        computed: {
            post () {
                return this.$store.state.post
            },
            paths(){
                return [{url: '/', name: '文章列表'}, {url: '', name: this.$store.state.post.title}]
            },
            comments(){
                return this.$store.state.comments
            }
        }
    }

</script>