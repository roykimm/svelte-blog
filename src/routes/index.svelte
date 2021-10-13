<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch('/posts.json')

        if(res.ok) {
            const { posts } = await res.json()
            return {
                props : { posts },
            }
        }
    }
</script>

<script>
    export let posts = []
</script>

<svelte:head>
    <title>Gobella Blog | Welcome</title>
</svelte:head>

<h1 class="text-2xl mt-5 mb-3 font-semibold text-center">
    안녕하세요 Gobella blog 입니다.
</h1>
<h4 class="text-sm text-center mb-5">
    python, react, linux등 에 관련 내용을 포스팅 합니다.
</h4>

<div class="grid grid-cols-1 md:grid-cols-2">
    {#each posts as {title, slug, excerpt, coverImage, tags}}
        <div class="card shadow-2xl mx-1 my-1">
            <figure class='px-10 pt-10'>
                <img class="rounded-xl h-96 md:h-48" src={coverImage.url} alt={`Cover image for ${title}`} />
            </figure>
            <div class="card-body">
                <h2 class="title text-md pb-3">{title}</h2>
                <p class="text-sm text-gray-500">{excerpt}</p>
                <div class="flex justify-center mt-5 space-x-2">
                    {#each tags as tag}
                        <span class="badge badge-primary px-2 pb-1 align-center">{tag}</span>
                    {/each}
                </div>
                <div class="justify-center card-actions">
                    <a href={`/posts/${slug}`} class="btn btn-outline btn-danger">Read More!</a>
                </div>
            </div>
        </div>
    {/each}
</div>
