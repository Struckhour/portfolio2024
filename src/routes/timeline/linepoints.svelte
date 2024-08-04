<script lang="ts">
    import { onMount } from 'svelte';
  
    let canvas: HTMLCanvasElement;
    let ctx: CanvasRenderingContext2D;
  
    function drawRibbon() {
        const width = canvas.width;
        const height = canvas.height;
        ctx.clearRect(0, 0, width, height);

        ctx.beginPath();
        ctx.moveTo(width / 2, 0);
        ctx.lineTo(width /2, height)
  
      ctx.strokeStyle = 'darkgreen'; // Tailwind 'blue-500'
      ctx.lineWidth = 2;
      ctx.stroke();
    }
  
    onMount(() => {
      canvas.width = canvas.clientWidth;
      canvas.height = canvas.clientHeight;
      ctx = canvas.getContext('2d') as CanvasRenderingContext2D;
      drawRibbon();
    });
  </script>
  
  <div class="w-full h-full flex items-center justify-center">
    <canvas bind:this={canvas} class="w-full h-full"></canvas>
  </div>