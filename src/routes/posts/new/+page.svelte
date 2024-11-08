<script>
    import { postsStore } from "$lib/stores/posts.js";
    import { goto } from "$app/navigation";

    let title = "";
    let content = "";
    let error = "";

    function handleSubmit() {
        if (title.length < 3) {
            error = "Title must be at least 3 characters long";
            return;
        }

        if (content.length < 10) {
            error = "Content must be at least 10 characters long";
            return;
        }

        postsStore.addPost({
            title,
            content,
        });

        title = "";
        content = "";
        error = "";

        goto("/posts");
    }
</script>

<h1 class="text-3xl font-bold mb-6">Create New Post</h1>

<form
    class="bg-white rounded-lg shadow-md p-6"
    on:submit|preventDefault={handleSubmit}
>
    {#if error}
        <div class="mb-4 p-4 bg-red-100 text-red-700 rounded-lg">
            {error}
        </div>
    {/if}
    <div class="space-y-6 mb-6">
        <div>
            <p class="mb-2">Title</p>
            <input
                type="text"
                class="w-full px-3 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                placeholder="Enter post title..."
                required
                bind:value={title}
            />
        </div>
        <div>
            <p class="mb-2">Description</p>
            <textarea
                class="w-full px-3 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
                rows="6"
                placeholder="Write your post content here..."
                required
                bind:value={content}
            ></textarea>
        </div>
    </div>
    <div class="flex justify-end gap-4">
        <a href="/posts" class="px-4 py-2 border rounded-lg hover:bg-gray-50">
            Cancel
        </a>
        <button
            type="submit"
            class="px-4 py-2 bg-blue-500 text-white rounded-lg hover:bg-blue-600"
        >
            Create Post
        </button>
    </div>
</form>
