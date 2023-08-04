<script>
	import { Container, Row, Col } from 'sveltestrap';
	import BreadcrumbOne from '@components/breadcrumbs/BreadcrumbOne.svelte';
	import TrialCard from '@view/dashboard/trial-project/TrialCard.svelte';

	const breadcrumbData = {
		pageTitle: 'Trial project',
		bcItem: 'Dashboard',
		bcItemActive: 'Trial Project'
	};
</script>

<svelte:head>
	<title>Trial project</title>
</svelte:head>

<div class="crm mb-25">
	<Container fluid>
		<Row>
			<Col xxl={12}>
				<BreadcrumbOne {...breadcrumbData} />
			</Col>
			<Col xxl={12} class="mb-25">
				<TrialCard />
			</Col>
		</Row>
	</Container>
</div>
