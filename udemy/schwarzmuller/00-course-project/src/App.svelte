<script>
    import Header from "./UI/Header.svelte";
    import MeetupGrid from "./Meetups/MeetupGrid.svelte";

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
</script>

<style>
    main {
        margin-top: 5rem;
    }
</style>

<Header />

<main>
    <form on:submit|preventDefault={addMeetup}>
        <div class='form-control'>
            <label for="title">Title</label>
            <input type="text" id='title' bind:value={title}/>
        </div>
        <div class='form-control'>
            <label for="subtitle">Subtitle</label>
            <input type="text" id='subtitle' bind:value={subtitle}/>
        </div>
        <div class='form-control'>
            <label for="description">Description</label>
            <textarea rows='3' id='description' bind:value={description}/>
        </div>
        <div class='form-control'>
            <label for="imageUrl;">Image URL</label>
            <input type="text" id='imageUrl' bind:value={imageUrl}/>
        </div>
        <div class='form-control'>
            <label for="address">Address</label>
            <input type="text" id='address' bind:value={address}/>
        </div>
        <div class='form-control'>
            <label for="email">E-Mail</label>
            <input type="email" id='email' bind:value={email}/>
        </div>
        <button type='submit'>Save</button>
    </form>
    <MeetupGrid {meetups}/>
</main>
