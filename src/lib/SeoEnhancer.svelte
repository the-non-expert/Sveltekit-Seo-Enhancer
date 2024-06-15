<script>
  import { onMount, onDestroy } from "svelte";
  import { tick } from "svelte";

  export let title = "";
  export let meta = [];
  export let link = [];
  export let script = [];
  export let jsonld = "";

  let headTags = [];

  function updateHead() {
    if (typeof document !== "undefined") {
      // Clear previous tags
      headTags.forEach((tag) => tag.remove());
      headTags = [];

      // Set title
      if (title) {
        document.title = title;
      }

      // Add meta tags
      meta.forEach((metaData) => {
        const metaTag = document.createElement("meta");
        Object.keys(metaData).forEach((key) => {
          metaTag.setAttribute(key, metaData[key]);
        });
        document.head.appendChild(metaTag);
        headTags.push(metaTag);
      });

      // Add link tags
      link.forEach(({ rel, href }) => {
        const linkTag = document.createElement("link");
        linkTag.setAttribute("rel", rel);
        linkTag.setAttribute("href", href);
        document.head.appendChild(linkTag);
        headTags.push(linkTag);
      });

      // Add script tags
      script.forEach(({ src, async, defer }) => {
        const scriptTag = document.createElement("script");
        scriptTag.setAttribute("src", src);
        if (async) scriptTag.setAttribute("async", "");
        if (defer) scriptTag.setAttribute("defer", "");
        document.head.appendChild(scriptTag);
        headTags.push(scriptTag);
      });

      // Add structured data (JSON-LD)
      if (jsonld) {
        const scriptTag = document.createElement("script");
        scriptTag.setAttribute("type", "application/ld+json");
        scriptTag.innerHTML = JSON.stringify(jsonld);
        document.head.appendChild(scriptTag);
        headTags.push(scriptTag);
      }
    }
  }

  onMount(updateHead);
  onDestroy(() => {
    if (typeof document !== "undefined") {
      headTags.forEach((tag) => tag.remove());
    }
  });

  $: tick().then(updateHead);
</script>

<slot></slot>
