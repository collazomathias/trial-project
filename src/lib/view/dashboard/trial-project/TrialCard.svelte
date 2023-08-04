<script>
	import { Card, CardHeader, CardBody } from 'sveltestrap';
</script>

<Card class="border-0">
	<CardHeader class="border-0 pb-md-0 pb-20">
		<h1>Fruits</h1>
	</CardHeader>
	<CardBody>
		<table>
            <thead>
                <tr>
                    <th>Fruit</th>
                    <th>Calories</th>
                    <th>Vitamin C</th>
                    <th>Potassium</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <td>Apple</td>
                    <td>52</td>
                    <td>4.6</td>
                    <td>107</td>
                </tr>
                <tr>
                    <td>Banana</td>
                    <td>89</td>
                    <td>8.7</td>
                    <td>358</td>
                </tr>
                <tr>
                    <td>Orange</td>
                    <td>47</td>
                    <td>53.2</td>
                    <td>181</td>
                </tr>
                <tr>
                    <td>Strawberry</td>
                    <td>32</td>
                    <td>58.8</td>
                    <td>153</td>
                </tr>
            </tbody>
        </table>
	</CardBody>
</Card>

<style lang="scss">
    
</style>
