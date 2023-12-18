<script>
    import { Line } from "svelte-chartjs";
    import { data } from './data.js';

    import {
        Chart as ChartJS,
        Title,
        Tooltip,
        Legend,
        LineElement,
        LinearScale,
        PointElement,
        CategoryScale,
    } from "chart.js";

    ChartJS.register(
        Title,
        Tooltip,
        Legend,
        LineElement,
        LinearScale,
        PointElement,
        CategoryScale,
    );
</script>

<Line {data} on:Resize={()=>console.log(111) } options={{ responsive: false }} />
