<script context="module">
    import ProjectCard from '$lib/components/project-card.svelte'
    import { client } from '$lib/graphql-client'
    import { projectsQuery } from '$lib/graphql-queries'

    export const load = async() => {
        const { projects } = await client.request(projectsQuery)
        return {
            props: {
                projects,
            },
        }
    }

</script>

<script>
    export let projects
</script>

<svelte:head>
    <title>My portfolio projects</title>
</svelte:head>

<h1 class="font-bold text-center mb-20 text-5xl">Recent Projects by Me</h1>

<div class="grip gap-10 md:grid-cols-4 md:px-10 lg:grid-cols-6 lg:-mx-52">
    {#each projects as { name, slug, description, image }, index}
    <ProjectCard {name} {description} url={image[0].url} {slug} />
    {/each}
</div>