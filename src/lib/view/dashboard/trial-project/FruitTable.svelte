<script>
    import { Card, CardHeader, CardBody } from 'sveltestrap';
    import { createEventDispatcher } from 'svelte';
    import Icon from '@iconify/svelte';
  
    export let data = [];
  
    // Creo el dispatcher de eventos
    const dispatch = createEventDispatcher();
  
    const editFruit = (fruit) => {
        dispatch('editFruit', fruit);
    }

    const deleteFruit = async(id) => {
        await fetch("http://localhost:8080/fruit/" + id, {
            method: 'DELETE'
        })
        .then((response) => {
            if (response.ok) {
                data = data.filter(fruit => fruit.id !== id);
            } else {
                console.error('Delete failed with status:', response.status);
            }
        })
        .catch((error) => {
            console.error('Delete error:', error);
        });
    }

</script>
  
<Card class="border-0">
    <CardHeader class="border-0 pb-md-0 pb-20">
        <h1>Fruits</h1>
    </CardHeader>
    <CardBody>
        <table>
            <thead>
            <tr>
                <th class="hidden">Id</th>
                <th>Fruit</th>
                <th>Calories</th>
                <th>Vitamin C</th>
                <th>Potassium</th>
                <th></th>
            </tr>
            </thead>
            <tbody>
            {#each data as {id, name, calories, vitaminC, potassium}}
                <tr>
                    <td class="hidden">{id}</td>
                    <td>{name}</td>
                    <td>{calories}</td>
                    <td>{vitaminC}</td>
                    <td>{potassium}</td>
                    <td>
                        <button on:click={() => editFruit({id, name, calories, vitaminC, potassium})}><Icon icon="uil:edit" style="font-size: 23px;" /></button>
                        <button class="delete-button" on:click={() => deleteFruit(id)}><Icon icon="tabler:trash" style="font-size: 23px;" /></button>
                    </td>
                </tr>
            {:else}
                <p>No results found...</p>
            {/each}
            </tbody>
        </table>
    </CardBody>
</Card>

<style lang="scss">
	@import '../../../../../static/css/variables.css';
    
    .hidden {
        display: none !important;
    }
    
    p {
        margin: 10px 0 0 10px;
    }

    table {
        width: 100%;
        border-collapse: collapse;
        border-radius: 8px;
        overflow: hidden;
    }

    tr:nth-of-type(even) {
        background: var(--tr-secondary-color);
    }

    thead {
        background: var(--table-primary-color) !important;
        color: var(--th-primary-color);
    }

    th {
        padding: 1.5em;
        padding-left: 0.8em;
        text-transform: uppercase;
    }

    td {
        width: 25%;
        padding: 0.8em;
        &:last-child {
            display: flex;
            gap: 10px;
            width: 105px !important;
        }
    }

    button {
        width: 35px;
        height: 35px;
        background: var(--button-primary-color);
        color: var(--button-text-color);
        font-weight: bold;
        border: none;
        border-radius: 8px;
        cursor: pointer;
        transition: all 0.3s ease-in-out;
        &:hover {
            background: var(--button-primary-color-hover);
        }
    }

    .delete-button {
        background: var(--clear-button-color);
        &:hover {
            background: var(--clear-button-color-hover);
        }
    }
</style>
