<script context="module">
    console.log('post!')
    export const load = async ({fetch, page: { params }}) => {
        
        const { slug }  = params;
        const res = await fetch(`/posts/${slug}.json`)

        if(res.ok) {
            const { post } = await res.json()
            console.log(post)
            return {
                props : { post },
            }
        }
    }
</script>

<script>
    export let post

    const { title, 
            date, 
            tags, 
            author: { name, authorTitle, picture} ,
            content: {html}, 
            coverImage 
          } = post
</script>

<svelte:head>
    <title>Gobella Blog | Welcome</title>
</svelte:head>

<div class="mb-5">
    <img 
        src={post.coverImage.url} 
        alt={`Cover image for ${title}`}
        class="w-screen"
    />
</div>

<h1 class="text-4xl font-semibold mb-5">{title}</h1>

<a href="/" class="inline-flex items-center mb-3">
    <img 
        src={picture.url} 
        alt={name}
        class="w-12 h-12 rounded-full flex-shrink-0 object-cover object-center"
    />
    <span class="flex-grow flex flex-col pl-4">
        <span class="title-font font-medium">{name}</span>
        <span class="text-secondary text-xs tracking-widest mt-0 5">
            {authorTitle}
        </span>
    </span>
</a>

<p class="text-secondary text-xs tracking-widest font-semibold">
    {new Date(date).toDateString()}
</p>

<div class="mb-5 flex justify-between">
    <div>
        {#if tags}
            <div class="mt-5 space-x-2">
                {#each tags as tag}
                    <span class="badge badge-primary pb-1">{tag}</span>
                {/each}
            </div>
        {/if}
    </div>
</div>

<article div class="prose pb-10">
    {@html html}
</article>