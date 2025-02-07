<script>
	import { io } from 'socket.io-client'
	let logs = []
	const socket = io(); 

	socket.on('serverLog', (data) => {
		if (data && data.message) {
			if (logs.length !== 0) {
				const message = data.message
				const now = new Date()
				now.setHours(now.getHours() + 1)
				const nowString = now.toISOString().replace('T', ' ').split('.')[0];
				const logMessage = `[${nowString}] ${message}`
				logs = [...logs, logMessage]
			} else {
				logs = [...logs, data.message]
			}
		}
	})
</script>

<div class="max-w-[90%] mx-auto mt-8 bg-gray-100 p-4 rounded-lg shadow w-full">
	<h3 class="text-lg font-semibold mb-4">Server Logs</h3>
	{#if logs.length != 0}
		<div
			class="max-w-[98%] mx-auto bg-white p-3 rounded-lg overflow-scroll whitespace-nowrap max-h-60">
			{#each logs as log}
				<p>{log}</p>
			{/each}
		</div>
	{/if}
</div>
