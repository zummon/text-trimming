<script>
	const options = ["Remove (parentheses)", "Spaces to one", "Space to tab"];
	const gen = (str, opt) => {
	  if (opt.includes(options[0])) {
	    str = str.replace(/ *\([^)]*\) */g, " ");
	  }
	  if (opt.includes(options[1])) {
	    str = str.replace(/  +/g, " ");
	  }
	  if (opt.includes(options[2])) {
	    str = str.replace(/ /g, "\t");
	  }
	  return str.trim();
	};

	let option = options.slice();
	let input = "";
	$: output = gen(input, option);
</script>

<div
	class="mx-auto mb-2 max-w-lg rounded-md border-2 border-dotted border-gray-500 px-2 py-1 text-center text-lg print:hidden"
>
	{#each options as value, i (`option-${i}`)}
		<label class="mr-2">
			<input type="checkbox" bind:group={option} {value} />
			{value}
		</label>
	{/each}
</div>

<div class="mx-auto flex max-w-3xl flex-wrap">
	<div class="w-full p-2 md:w-1/2">
		<h2 class="mb-2 text-xl font-semibold">Input</h2>
		<textarea
			class="w-full resize-none text-black"
			rows="10"
			bind:value={input}
			placeholder="text to work on..."
		/>
	</div>
	<div class="w-full p-2 md:w-1/2">
		<h2 class="mb-2 text-xl font-semibold">Result</h2>
		<textarea
			class="w-full resize-none text-black"
			rows="10"
			value={output}
			readonly
			placeholder="input the first box first"
			onclick="this.select()"
		/>
		Select and copy manually
	</div>
</div>
