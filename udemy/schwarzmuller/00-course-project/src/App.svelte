<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";
    import TextInput from "./UI/TextInput.svelte";
    import Button from "./UI/Button.svelte";
  import { missing_component } from "svelte/internal";

    let title = '';
    let subtitle = '';
    let description = '';
    let imageUrl = '';
    let address = '';
    let email = '';

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

    function addMeetup() {
        const newMeetup = {
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageUrl: imageUrl,
            address: address,
            contactEmail: email

        }

        meetups = [newMeetup, ...meetups]
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
</script>

<style>
    main {
        margin-top: 5rem;
    }

    form {
        width: 30rem;
        max-width: 90%;
        margin: auto
    }
</style>

<Header />

<main>
    <form on:submit|preventDefault={addMeetup}>
        <TextInput
            id="title"
            label="Title"
            value={title}
            on:input={event => title = event.target.value}
        />
        <TextInput
            id="subtitle"
            label="Subtitle"
            value={subtitle}
            on:input={event => subtitle = event.target.value}
        />
        <TextInput
            id="description"
            controlType="textarea"
            label="Description"
            rows=3
            value={description}
            on:input={event => description = event.target.value}
        />
        <TextInput
            id="imageUrl"
            label="Image URL"
            value={imageUrl}
            on:input={event => imageUrl = event.target.value}
        />
        <TextInput
            id="address"
            label="Address"
            value={address}
            on:input={event => address = event.target.value}
        />
        <TextInput
            id="email"
            label="E-Mail"
            value={email}
            type="email"
            on:input={event => email = event.target.value}
        />
        <Button
            type="submit"
            caption="Save"
        />
    </form>
    <MeetupGrid {meetups} on:togglefavourite={toggleFavourite}/>
</main>
