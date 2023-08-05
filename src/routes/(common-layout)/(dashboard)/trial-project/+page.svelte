<script>

	import { Container, Row, Col } from 'sveltestrap';
	import BreadcrumbOne from '@components/breadcrumbs/BreadcrumbOne.svelte';
	import FruitTable from '@view/dashboard/trial-project/FruitTable.svelte';
	import FruitForm from '../../../../lib/view/dashboard/trial-project/FruitForm.svelte';
	import { onMount } from 'svelte';

	const breadcrumbData = {
	  pageTitle: 'Trial project',
	  bcItem: 'Dashboard',
	  bcItemActive: 'Trial project'
	};
  
	// Creo la variable para guardar la fruta seleccionada
	let selectedFruit = {};

	let data = [];

    async function fetchData() {
        await fetch("http://localhost:8080/fruit")
		.then(response => response.json())
		.then(fruits => {
			data = fruits;
		});
    }

    function handleEdit(event) {
		selectedFruit = event.detail;
    }

	onMount(() => {
		fetchData();
	});

	const handleFruitsUpdated = (event) => {
		data = event.detail;
	};
	
  </script>

<svelte:head>
	<title>Trial Project</title>
</svelte:head>

<div class="crm mb-25">
	<Container fluid>
		<Row>
			<Col xxl={12}>
				<BreadcrumbOne {...breadcrumbData} />
			</Col>
			<Col xxl={9}>
				<!-- Obtengo los datos seleccionados del componente FruitTable -->
				<FruitTable {data} on:editFruit={handleEdit} />
			  </Col>
			  <Col xxl={3}>
				<!-- Paso los datos de la fruta seleccionada al componente FruitForm -->
				<FruitForm {data} {...selectedFruit} on:fruitsUpdated={handleFruitsUpdated} />
			  </Col>
		</Row>
	</Container>
</div>
