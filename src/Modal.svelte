
<script>
    export let modalStyle = '';
    export let errorMessage = '';
    export let closeModal;
  </script>
  
  <div class="modal" tabindex="-1" role="dialog" style="{modalStyle}">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">Error</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close" on:click={closeModal}>
           
          </button>
        </div>
        <div class="modal-body">
          {errorMessage}
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-dismiss="modal" on:click={closeModal}>Close</button>
        </div>
      </div>
    </div>
  </div>
  
  <style>
  
  </style>
  