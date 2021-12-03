<script>
	import data from '../data/top10.json';
	import { extent, scaleLinear, groups, scaleBand, scaleOrdinal, schemeCategory10 } from 'd3';

	let width = 0;
	const HEIGHT = 500;
	const RADIUS = 10;
	const margins = {
		top: 10,
		right: 10,
		bottom: 10,
		left: 200
	};

	$: bounds = {
		width,
		height: HEIGHT,
		chartWidth: width - margins.left - margins.right,
		chartHeight: HEIGHT - margins.top - margins.bottom
	};

	// X
	$: xDomain = extent(data, (d) => d.performance);
	$: xScale = scaleLinear().domain(xDomain).range([0, bounds.chartWidth]);
	// Y
	$: yDomain = [...new Set(data.map((d) => d.Name))];
	$: yScale = scaleBand().domain(yDomain).range([bounds.chartHeight, 0]);

	// Color
	$: colorScale = scaleOrdinal()
		.domain([...new Set(data.map((d) => d.skill))])
		.range(schemeCategory10);

	// Data
	$: players = groups(data, (d) => d.Name);

	$: console.log(players);
</script>

<div bind:clientWidth={width}>
	<svg width={bounds.width} height={bounds.height}>
		{#each players as player}
			<g transform={`translate(0, ${yScale(player[0])})`}>
				<text>{player[0]}</text>
				<g>
					{#each player[1] as skill}
						<circle
							cx={xScale(skill.performance)}
							cy={0}
							r={RADIUS}
							fill={colorScale(skill.skill)}
						/>
					{/each}
				</g>
			</g>
		{/each}
	</svg>
</div>
