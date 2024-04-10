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
					row.push({
						row: i,
						col: j,
						index: i === 0 && j === 0 ? '' : i === 0 ? j : i,
						highlighted: false
					});
				} else {
					// 積を表示する
					row.push({ row: i, col: j, product: i * j, highlighted: false });
				}
			}
			gridData.push(row);
		}
		return gridData;
	}

	// グリッドのデータを取得
	let gridData = generateGridData(rows, cols);

	// セルをクリックしたときのハンドラ
	function cellClicked(row, col) {
		if (row > 0 && col > 0) gridData[row][col].highlighted = !gridData[row][col].highlighted;
	}
</script>

<div class="grid">
	{#each gridData as row, rowIndex}
		{#each row as cell, colIndex}
			<div
				class="cell"
				on:click={() => cellClicked(cell.row, cell.col)}
				class:highlighted={cell.highlighted}
			>
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
		cursor: pointer;
	}
	.highlighted {
		background-color: yellow;
	}
</style>
