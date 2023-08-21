<script type="text/javascript">
  let file
  let src


  function dragMe(node) {
     let moving = false;
     let left = 300;
     let top = 100;
     let width = 100;

     node.style.position = 'absolute';
     node.style.top = `${top}px`;
     node.style.left = `${left}px`;
     node.style.width = `${width}px`;
     node.style.cursor = 'move';
     node.style.userSelect = 'none';

     node.addEventListener('mousedown', () => {
       moving = true;
     });

    window.addEventListener('mousemove', (e) => {
      if (e.shiftKey) {
        width += e.movementX
        node.style.width = `${width}px`;
      } else if (moving) {
        left += e.movementX;
        top += e.movementY;
        node.style.top = `${top}px`;
        node.style.left = `${left}px`;
      }
     });

     window.addEventListener('mouseup', () => {
       moving = false;
     });

  }

  function on_file_input(e) {
    file = (e.target).files?.[0];
    let reader = new FileReader();
    reader.readAsDataURL(file);
    reader.onload = e => {
      src = e.target.result
    }
  }
</script>

<figure use:dragMe>
  <img src={src}>
</figure>

<details>
  <summary>
    Image
  </summary>

  <div class="controls">
    <form>
      <input
        on:input="{on_file_input}"
        type="file"
        name="file"
        accept="image/png, image/jpeg">
    </form>
  </div>
</details>


<style type="text/css">
  details {
    position: absolute;
    right: 1rem;
    top: 1rem;
  }
  figure {
    position: absolute;
    top: 5px;
    margin: 0;
/*    z-index: -1;*/
  }
  img {
    max-width: 100%;
    pointer-events: none;
  }

  .controls {
    position: absolute;
    right: 0;
    z-index: 200;
    background-color: white;
    border: 2px solid black;
    padding: 1rem;
  }
</style>