<script>

    import { Card, CardHeader, CardBody } from 'sveltestrap';
    import Icon from '@iconify/svelte';
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();

    export let data;

    export let id = null;
    export let name = null;
    export let calories = null;
    export let vitaminC = null;
    export let potassium = null;

    const addFruit = async() => {
        await fetch("http://localhost:8080/fruit", {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                name: name,
                calories: calories,
                vitaminC: vitaminC,
                potassium: potassium
            })
        })
        .then(response => response.json())
        .then(fruit => {
            data.push({
                id: fruit.id,
                name: fruit.name,
                calories: fruit.calories,
                vitaminC: fruit.vitaminC,
                potassium: fruit.potassium
            });
            dispatch('fruitsUpdated', data);
            clearForm();
        });
    }

    const editFruit = async() => {
        await fetch("http://localhost:8080/fruit/" + id, {
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify({
                name: name,
                calories: calories,
                vitaminC: vitaminC,
                potassium: potassium
            })
        }).then(response => response.json())
        .then(fruit => {
            const index = data.findIndex(f => f.id === fruit.id);
            if (index !== -1) {
                data[index] = {
                    id: fruit.id,
                    name: fruit.name,
                    calories: fruit.calories,
                    vitaminC: fruit.vitaminC,
                    potassium: fruit.potassium
                };
            }
            dispatch('fruitsUpdated', data);
            clearForm();
        });
    }
    
    const clearForm = () => {
        id = null;
        name = null;
        calories = null;
        vitaminC = null;
        potassium = null;
    }

</script>

<Card class="border-0">
    <CardHeader class="border-0 pb-md-0 pb-20">
        {#if id === null}
            <h1>Add Fruit</h1>
        {:else}
            <h1>Edit Fruit</h1>
        {/if}
    </CardHeader>
    <CardBody>
        <form on:submit={(id === null) ? addFruit : editFruit}>
            <input type="text" id="fruitId" name="fruitId" bind:value={id} hidden>
            <label for="fruitName">Fruit name</label>
            <input type="text" id="fruitName" name="fruitName" placeholder="Enter a fruit name..." bind:value={name} minlength="3" maxlength="30" required>
            <label for="fruitCalories">Fruit calories</label>
            <input type="number" step="any" id="fruitCalories" name="fruitCalories" placeholder="Enter the calories..." bind:value={calories} min="0" required>
            <label for="fruitVitaminC">Fruit vitamin C</label>
            <input type="number" step="any" id="fruitVitaminC" name="fruitVitaminC" placeholder="Enter the vitamin C..." bind:value={vitaminC} min="0" required>
            <label for="fruitPotassium">Fruit potassium</label>
            <input type="number" step="any" id="fruitPotassium" name="fruitPotassium" placeholder="Enter the potassium..." bind:value={potassium} min="0" required>
            <div>
                {#if id === null}
                    <button type="submit"><Icon icon="gala:add" style="font-size: 23px;" />Add fruit</button>
                {:else}
                    <button type="submit"><Icon icon="uil:edit" style="font-size: 23px;" />Edit fruit</button>
                {/if}
                <button type="reset" on:click={() => clearForm()} class="clear-form"><Icon icon="carbon:clean" style="font-size: 23px;" /></button>
            </div>
        </form>
    </CardBody>
</Card>

<style lang="scss">
	@import '../../../../../static/css/variables.css';

    input {
        width: 100%;
        border-radius: 4px;
        height: 35px;
        border: 1px solid var(--new-input-border-color);
        outline: none;
        padding-left: 10px;
        margin-bottom: 15px;
        color: var(--new-input-border-color);
    }

    label {
        color: var(--new-title-primary-color);
        font-weight: bold;
    }

    div {
        width: 100%;
        display: flex;
        gap: 10px;
        height: 30px;
    }

    button {
        display: flex;
        place-items: center;
        place-content: center;
        gap: 10px;
        border-radius: 8px;
        height: 35px;
        width: 130px;
        font-weight: bold;
        border: none;
        outline: none;
        color: var(--button-text-color);
        background-color: var(--button-primary-color);
        transition: 0.3s ease-in-out;
        &:hover {
            background: var(--button-primary-color-hover);
        }
    }

    .clear-form {
        width: 35px !important;
        background-color: var(--clear-button-color);
        transition: 0.3s ease-in-out;
        &:hover {
            background: var(--clear-button-color-hover);
        }
    }

</style>