<script>
    import Header from "./UI/Header.svelte";
    import MeetupItem from "./Meetups/MeetupItem.svelte";

    const meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code',
            imageUrl: 'https://theforage.wpengine.com/wp-content/uploads/2023/02/Best-coding-bootcamps-online.jpg',
            address: '27 Nerd Road, 38236 New York',
            contactEmail: 'code@test.com'
        },
        {
            id: 'm2',
            title: 'Swim Together',
            subtitle: 'Let\'s go swim!',
            description: 'We will simply swim some laps',
            imageUrl: 'https://secure.meetupstatic.com/photos/event/2/5/4/5/600_510609541.webp?w=750',
            address: '123 Pool Road, 38221 Boston',
            contactEmail: 'swim@test.com'
        }
    ];
</script>

<style>
    #meetups {
        margin-top: 5rem;
    }
</style>

<Header />

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
        />
    {/each}
</section>
