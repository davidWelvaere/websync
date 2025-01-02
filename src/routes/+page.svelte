<script>
	export let elfsquadClientId = "defaultClientId";
	export let elfsquadClientSecret = "defaultClientSecret";
	export let odooUrl = "https://example.com";
	export let odooDb = "defaultDb";
	export let odooUsername = "defaultUser";
	export let odooPassword = "defaultPassword";
	export let odooFields = "defaultField1,defaultField2";
	export let validateUuid = false;
	export let fullSync = false;
	export let logs = [];

	function handleSubmit(event) {
		event.preventDefault();
		const data = {
			elfsquadClientId,
			elfsquadClientSecret,
			odooUrl,
			odooDb,
			odooUsername,
			odooPassword,
			odooFields,
			validateUuid,
			fullSync,
		};
		const timestamp = new Date().toLocaleString();
		console.log("Form submitted!", data);
		logs = [
			...logs,
			`[${timestamp}] Form submitted with data: ${JSON.stringify(data)}`,
		];
	}
</script>

<div class="max-w-lg mx-auto bg-white p-6 rounded-lg shadow-lg">
	<h2 class="text-2xl font-bold text-center mb-6">Odoo-Elfsquad Sync Form</h2>
	<form on:submit={handleSubmit} class="space-y-4">
		<!-- Elfsquad Authentication -->
		<div>
			<label
				for="elfsquadClientId"
				class="block text-sm font-medium text-gray-700"
				>Elfsquad Client ID</label>
			<input
				type="text"
				id="elfsquadClientId"
				bind:value={elfsquadClientId}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>
		<div>
			<label
				for="elfsquadClientSecret"
				class="block text-sm font-medium text-gray-700"
				>Elfsquad Client Secret</label>
			<input
				type="password"
				id="elfsquadClientSecret"
				bind:value={elfsquadClientSecret}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>

		<!-- Odoo Authentication -->
		<div>
			<label for="odooUrl" class="block text-sm font-medium text-gray-700"
				>Odoo URL</label>
			<input
				type="url"
				id="odooUrl"
				bind:value={odooUrl}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>
		<div>
			<label for="odooDb" class="block text-sm font-medium text-gray-700"
				>Odoo Database Name</label>
			<input
				type="text"
				id="odooDb"
				bind:value={odooDb}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>
		<div>
			<label
				for="odooUsername"
				class="block text-sm font-medium text-gray-700"
				>Odoo Username</label>
			<input
				type="text"
				id="odooUsername"
				bind:value={odooUsername}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>
		<div>
			<label
				for="odooPassword"
				class="block text-sm font-medium text-gray-700"
				>Odoo Password</label>
			<input
				type="password"
				id="odooPassword"
				bind:value={odooPassword}
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500" />
		</div>

		<!-- Odoo Fields to Sync -->
		<div>
			<label
				for="odooFields"
				class="block text-sm font-medium text-gray-700"
				>Odoo Fields to Sync</label>
			<textarea
				id="odooFields"
				bind:value={odooFields}
				rows="5"
				required
				class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:ring-blue-500 focus:border-blue-500"
				placeholder="Enter Odoo fields to sync, separated by commas."
			></textarea>
		</div>

		<!-- Sync Options -->
		<div class="flex items-center">
			<input
				type="checkbox"
				id="validateUuid"
				bind:checked={validateUuid}
				class="h-4 w-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500" />
			<label for="validateUuid" class="ml-2 block text-sm text-gray-700"
				>Check validity of Elfsquad UUID</label>
		</div>
		<div class="flex items-center">
			<input
				type="checkbox"
				id="fullSync"
				bind:checked={fullSync}
				class="h-4 w-4 text-blue-600 border-gray-300 rounded focus:ring-blue-500" />
			<label for="fullSync" class="ml-2 block text-sm text-gray-700"
				>Perform full sync</label>
		</div>

		<button
			type="submit"
			class="w-full py-2 px-4 bg-blue-600 text-white font-medium text-sm rounded-md shadow-sm hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2">
			Submit
		</button>
	</form>
</div>

<div class="max-w-lg mx-auto mt-8 bg-gray-100 p-4 rounded-lg shadow">
	<h3 class="text-lg font-semibold mb-4">Server Logs</h3>
	<ul class="space-y-2">
		{#each logs as log}
			<li class="text-sm text-gray-700 bg-white p-2 rounded shadow">
				<span class="font-mono text-gray-500">{log}</span>
			</li>
		{/each}
	</ul>
</div>

