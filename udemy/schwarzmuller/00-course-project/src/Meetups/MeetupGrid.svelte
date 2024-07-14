<script>
    import MeetupItem from "./MeetupItem.svelte";

    export let meetups;
</script>

<style>
    section {
        width: 100%;
        display: grid;
        grid-template-columns: 1fr;
        grid-gap: 1rem;
    }

    @media (min-width: 768px) {
        section {
            grid-template-columns: repeat(2, 1fr);
        }
    }
</style>

<section id='meetups'>
    {#each meetups as m}
        <MeetupItem
            id={m.id}
            title={m.title}
            subtitle={m.subtitle}
            description={m.description}
            imageUrl={m.imageUrl}
            address={m.address}
            email={m.contactEmail}
            isFav={m.isFavourite}
            on:togglefavourite
        />
    {/each}
</section>