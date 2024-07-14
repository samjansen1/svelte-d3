<script>
    import { createEventDispatcher } from 'svelte';
    import TextInput from "../UI/TextInput.svelte";
    import Button from "../UI/Button.svelte";
    import Modal from '../UI/Modal.svelte';

    let title = '';
    let subtitle = '';
    let description = '';
    let imageUrl = '';
    let address = '';
    let email = '';

    const dispatch = createEventDispatcher();

    function submitForm() {
        dispatch('save', {
            title: title,
            subtitle: subtitle,
            address: address,
            description: description,
            email: email,
            imageUrl: imageUrl
        })
    }
</script>

<style>
    form {
        max-width: 100%;
    }
</style>

<Modal title='Edit Meetup Data' on:cancel>
    <form on:submit|preventDefault={submitForm}>
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
    </form>
</Modal>
