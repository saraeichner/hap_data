<script>
    // based on suggestions from:
    // Inclusive Components by Heydon Pickering https://inclusive-components.design/collapsible-sections/
    export let headerText;

    // create prop to track whether or not the section is visible
    export let isVisible = true;
    let expanded = isVisible;
    let isDesktop = window.innerWidth >= 768; 

    // Function to update expanded and isVisible based on screen width
    function updateVisibility() {
      isDesktop = window.innerWidth >= 768; // Adjust the breakpoint as needed
      expanded = isDesktop && isVisible;
    }

    // Initial call to set the initial values based on the screen width
    updateVisibility();

    // Event listener to update values on window resize
    window.addEventListener('resize', updateVisibility);
</script>

<div class="collapsible">
    <h3>
      <button aria-expanded={expanded} on:click={() => expanded = !expanded}>
        {#if headerText}
            <!-- {headerText} -->
            <span class="header-text {expanded ? 'expanded' : ''}" >{headerText}</span>
          {/if}
        {#if expanded}
          <!-- "X" SVG for close -->
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          </svg>
        {:else}
          <!-- "+" SVG for open -->
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <line x1="12" y1="5" x2="12" y2="19"></line>
            <line x1="5" y1="12" x2="19" y2="12"></line>
          </svg>
        {/if}
    </h3>
    
    <div class='contents' hidden={!expanded}>
        <slot></slot>
    </div>
</div>

<style>
  .collapsible {
    border-bottom: 1.5px solid var(--gray-light, #e1e1e1);
    display: flex;
    flex-direction: column;
    overflow-y: hidden;
  }

  /* Hide scrollbar for Chrome, Safari and Opera */
	.collapsible::-webkit-scrollbar,
  .contents::-webkit-scrollbar {
		display: none;
	}

	/* Hide scrollbar for IE, Edge and Firefox */
	.collapsible::-webkit-scrollbar,
  .contents {
		-ms-overflow-style: none;  /* IE and Edge */
		scrollbar-width: none;  /* Firefox */
	}
	
	h3 {
		margin: 0;
	}

.collapsible h3 .header-text.expanded {
  /* Styles for expanded state */
  color: #3884CB;
}

.contents {
   overflow-y: scroll;
   flex-grow: 1;
}
	
  button {
    background-color: var(--background, #fff);
    color: var(--gray-darkest, #999);
    display: flex;
		justify-content: space-between;
    width: 100%;
		border: none;
		margin: 0;
		padding: 0.5em 0.5em;
    font-family: "ff-tisa-sans-web-pro", sans-serif;
    /* font-size: 9pt;
    color: #999; */
    font-size: 16pt;
    font-weight: 600;
    color: #666;
    padding: 15px;
  }

  /* Target span element within button */
  .collapsible h3 button > .header-text {
    text-align: left;
  }

  @media (max-width: 1000px) {
    button {
      font-size: 18px;
    }
  }

  @media (max-width: 900px) {
    button {
      font-size: 16px;
    }
  }

  /* Media query for mobile devices */
	@media (max-width: 767px) {
    button {
      font-size: 18px;
      padding-top: 0.3em;
      padding-bottom: 0.3em;
      padding: 3px 11px 3px 11px; /* this adjusts the padding arond site amenity*/
    }

    .contents {
      max-height: 150px
    }
  }


  /* button[aria-expanded="true"] {
    border-bottom: 1.5px solid var(--gray-light, #e1e1e1);
  } */

</style>