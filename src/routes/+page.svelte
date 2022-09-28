<script type="typescript">
import { onMount } from 'svelte';

type Posts = {
    postId: number,
    id: number,
    name: string,
    email: string,
    body: string
}
let posts: Array<Posts> = []
let loading = false
onMount(async () => {
    loading = true
	const res = await fetch('https://jsonplaceholder.typicode.com/comments');
	posts = await res.json();
    loading = false
});

const goToTop = () => {
    console.log('go to top')
    window.scrollTo(0, 0)
}

</script>


<se-loading loading={loading}></se-loading>
<se-fab option="backtotop" on:click={goToTop}></se-fab>
  <se-container display="flex" padding="large">
    <se-block margin="large">
        <se-block-header>Posts</se-block-header>
        <se-block-content>
            <se-link url="/about">Go to About page</se-link>
            {#each posts as post}
                <se-block option="card">
                    <se-block-header>Name - {post.name} - {post.email}</se-block-header>
                    <se-block-content>{post.body}</se-block-content>
                    <se-block-footer>{post.id}</se-block-footer>
                </se-block>
            {/each}
        </se-block-content>
        <se-block-footer>
            Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
        </se-block-footer>
    </se-block>
    <se-block>
  </se-block>
</se-container>