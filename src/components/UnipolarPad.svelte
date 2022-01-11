<script context="module">
  import Conversion    from 'svelte-coordinate-conversion'
  import DragDropTouch from 'svelte-drag-drop-touch'
</script>

<script>
  import { onMount } from 'svelte';
  let Arena, DragImage;
  let barSize = 35;
  let X = 20, maxX = 400-barSize, DeltaX; 
  const minX = 0, minY =0;
  let Y = 20, maxY = 400, DeltaY; 
  let PositioningWasDelayed = false // workaround for problem with "drag" events
  export let currentValue = 0;;

   onMount(async()=>{
        barSize = window.screen.width / 15;
        maxX = window.screen.width * 0.8 - barSize;
        maxY = window.screen.width * 0.8;
        const root = document.documentElement;
        root.style.setProperty('--screen-width', window.screen.width * 0.8 + "px");
   })

  function startDragging (Event) {
    let TargetBox = Event.target.getBoundingClientRect()
      DeltaX = Event.pageX - TargetBox.left-window.scrollX
      DeltaY = Event.pageY - TargetBox.top-window.scrollY
    PositioningWasDelayed = false

    DragImage = document.createElement('div')       // width/height must be > 0!
      DragImage.setAttribute(
        'style','display:block; position:absolute; width:1px; height:1px'
      )
      document.body.appendChild(DragImage)
    Event.dataTransfer.setDragImage(DragImage, 0,0)
    Event.dataTransfer.effectAllowed = 'move'
  }

  function continueDragging (Event) {
    if ((Event.screenX === 0) && (Event.screenY === 0) && ! PositioningWasDelayed) {
      PositioningWasDelayed = true   // last "drag" event contains wrong coord.s
    } else {
      PositioningWasDelayed = false

      let localPosition = Conversion.fromDocumentTo(
        'local',{ left:Event.pageX-DeltaX, top:Event.pageY-DeltaY },Arena
      )
      X = Math.max(minX, Math.min(maxX, localPosition.left))
      Y = Math.max(minY, Math.min(maxY, localPosition.top))
			currentValue = Math.ceil((X * 18) / maxX) -4;
			currentValue = currentValue < 0 ? 0 : currentValue
    }

    Event.dataTransfer.dropEffect = 'move'
    Event.stopPropagation()
  }

  function finishDragging (Event) {
    document.body.removeChild(DragImage)    // works with older browsers as well
    Event.stopPropagation()
  }
</script>
<div class="pad-wrapper">
    <div bind:this={Arena} id="arena">
    <div draggable="true" style="
        display:block; position:absolute;
        left:{X}px; top:{0}px; width:{barSize}px; height:100%;
        background:forestgreen; color:white;
        line-height:30px; text-align:center;
        cursor:move;
        " on:dragstart={startDragging} on:drag={continueDragging} on:dragend={finishDragging}
        >
        {currentValue}
        </div>
    </div>
</div>

<style>
  div {
    -webkit-touch-callout:none;
    -ms-touch-action:none; touch-action:none;
  }
	#arena {
		display:block; 
		position:relative;
  	    width:var(--screen-width);
		height:var(--screen-width);
  	    margin:20px;
  	    border:dotted 1px black;
		border-radius:4px;
	}
	#arena:after{
		position:absolute;
		top:0px;
		left:90px;
		width:0px;
		min-height:var(--screen-width);
		pointer-events:none;
		content:'';
		outline:red solid 1px;
	}
</style>

