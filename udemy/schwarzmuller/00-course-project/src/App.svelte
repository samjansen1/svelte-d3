<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import EditMeetup from "./Meetups/EditMeetup.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";
  import { missing_component } from "svelte/internal";

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle: 'Learn to code in 2 hours',
            description: 'In this meetup, we will have some experts that teach you how to code',
            imageUrl: 'https://theforage.wpengine.com/wp-content/uploads/2023/02/Best-coding-bootcamps-online.jpg',
            address: '27 Nerd Road, 38236 New York',
            contactEmail: 'code@test.com',
            isFavourite: false
        },
        {
            id: 'm2',
            title: 'Swim Together',
            subtitle: 'Let\'s go swim!',
            description: 'We will simply swim some laps',
            imageUrl: 'https://secure.meetupstatic.com/photos/event/2/5/4/5/600_510609541.webp?w=750',
            address: '123 Pool Road, 38221 Boston',
            contactEmail: 'swim@test.com',
            isFavourite: false
        }
    ];

    let editMode = null;

    function addMeetup(event) {
        const newMeetup = {
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            address: event.detail.address,
            contactEmail: event.detail.email,
            isFavourite: false
        }

        meetups = [newMeetup, ...meetups];
        editMode = null;
    }

    function toggleFavourite(event) {
        const id = event.detail;
        const updatedMeetup = {...meetups.find(m => m.id === id)};
        updatedMeetup.isFavourite = !updatedMeetup.isFavourite;
        const meetupIndex = meetups.findIndex(m => m.id === id)
        const updatedMeetups = [...meetups]
        updatedMeetups[meetupIndex] = updatedMeetup;
        meetups = updatedMeetups;
    }

    function cancelEdit() {
        editMode = null;
    }
</script>

<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;
    }
</style>

<Header />

<main>
    <div class='meetup-controls'>
        <Button on:click={() => editMode = 'add'}>New Meetup</Button>
    </div>
    {#if editMode === 'add'}
        <EditMeetup on:save={addMeetup} on:cancel={cancelEdit}/>
    {/if}
    <MeetupGrid {meetups} on:togglefavourite={toggleFavourite}/>
</main>
