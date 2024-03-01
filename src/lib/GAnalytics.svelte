<script lang="ts">
    import { page } from '$app/stores'
    // import gtag from '@types/gtag.js'
  
    $: {
      if (typeof gtag !== 'undefined') {
        gtag('config', 'G-CHPXB0GBLV', {
          page_title: document.title,
          page_path: $page.url.pathname,
        })
      }
    }
  </script>
  
  <svelte:head>
    <script
      async
      src="https://www.googletagmanager.com/gtag/js?id=G-CHPXB0GBLV">
    </script>
    <script>
      window.dataLayer = window.dataLayer || []
  
      function gtag() {
        dataLayer.push(arguments)
      }
  
      gtag('js', new Date())
      gtag('config', 'G-CHPXB0GBLV')
    </script>
  </svelte:head>
  