<script>
	// グリッドの行数と列数
	const rows = 13;
	const cols = 13;

	// グリッドのセルのデータを生成する関数
	function generateGridData(rows, cols) {
		const gridData = [];
		for (let i = 0; i < rows; i++) {
			const row = [];
			for (let j = 0; j < cols; j++) {
				if (i === 0 || j === 0) {
					// 行番号と列番号を表示する
					row.push({ row: i, col: j, index: i === 0 && j === 0 ? '' : i === 0 ? j : i });
				} else {
					// 積を表示する
					row.push({ row: i, col: j, product: i * j });
				}
			}
			gridData.push(row);
		}
		return gridData;
	}

	// グリッドのデータを取得
	const gridData = generateGridData(rows, cols);
</script>

<div class="grid">
	{#each gridData as row, rowIndex}
		{#each row as cell, colIndex}
			<div class="cell">
				{#if cell.index !== undefined}
					<span>{cell.index}</span>
				{:else}
					<span>{cell.product}</span>
				{/if}
			</div>
		{/each}
	{/each}
</div>

<style>
	.grid {
		display: grid;
		grid-template-columns: repeat(13, 1fr);
		grid-gap: 2px;
		background-color: #ddd;
		padding: 10px;
	}
	.cell {
		background-color: white;
		border: 1px solid #aaa;
		padding: 20px;
		text-align: center;
	}
</style>
