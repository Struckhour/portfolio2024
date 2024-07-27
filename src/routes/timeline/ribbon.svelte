<!-- RibbonCanvas.svelte -->
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

        const numberOfCurves = 6;
        const curveHeight = height / numberOfCurves;
        const rightOffshootLengths = [10, -25, 3, -12, 15, 3];
        const leftOffshootLengths = [22, -1, 23, -18, 15, 3];
        const rightBranches = [0, 1, 2, 3, 4, ]
        const leftBranches = [0, 1, 2, 3]


        for (let i = 0; i < numberOfCurves; i++) {
            let offshootControlPointX = 0;
            let offshootControlPointY = 0;
            let offshootEndPointX = 0;
            let offshootEndPointY = 0;
            const controlPointX = width / 2 + (i % 2 === 0 ? 50 : -50);
            const controlPointY = (i + 0.5) * curveHeight;
            const endPointX = width / 2;
            const endPointY = (i + 1) * curveHeight;
    
            ctx.quadraticCurveTo(controlPointX, controlPointY, endPointX, endPointY);

            if (leftBranches.includes(i)) {
                offshootControlPointX = endPointX - 40 + leftOffshootLengths[i];
                offshootControlPointY = endPointY - 80 + leftOffshootLengths[i];
                offshootEndPointX = endPointX - 80 + leftOffshootLengths[i];
                offshootEndPointY = endPointY - 40 + leftOffshootLengths[i];
                ctx.quadraticCurveTo(offshootControlPointX, offshootControlPointY, offshootEndPointX, offshootEndPointY);
            }
            ctx.moveTo(endPointX, endPointY);
            if (rightBranches.includes(i)) {
                offshootControlPointX = endPointX + 40 + rightOffshootLengths[i];
                offshootControlPointY = endPointY - 60 + rightOffshootLengths[i];
                offshootEndPointX = endPointX + 70 + rightOffshootLengths[i];
                offshootEndPointY = endPointY - 40 + rightOffshootLengths[i];
            ctx.quadraticCurveTo(offshootControlPointX, offshootControlPointY, offshootEndPointX, offshootEndPointY);
            }
            ctx.moveTo(endPointX, endPointY);
        }
  
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
  
  <div class="w-full h-[1000px] flex items-center justify-center">
    <canvas bind:this={canvas} class="w-full h-full"></canvas>
  </div>