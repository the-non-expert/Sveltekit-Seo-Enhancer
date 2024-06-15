<script>
  import SeoEnhancer from "$lib/SeoEnhancer.svelte";

  let product = {
    name: "Awesome Product",
    description: "This is an awesome product.",
    url: "https://www.example.com/product/awesome",
    imageUrl: "https://www.example.com/product/awesome.jpg",
    price: "119.99",
    currency: "USD",
    brand: "ACME",
  };

  let metaTags = [
    { name: "description", content: product.description },
    { property: "og:title", content: product.name },
    { property: "og:description", content: product.description },
    { property: "og:url", content: product.url },
    { property: "og:image", content: product.imageUrl },
  ];
</script>

<SeoEnhancer
  title={product.name}
  meta={metaTags}
  link={[{ rel: "canonical", href: product.url }]}
  jsonld={{
    "@context": "https://schema.org",
    "@type": "Product",
    name: product.name,
    image: product.imageUrl,
    description: product.description,
    sku: "0446310786",
    brand: {
      "@type": "Brand",
      name: product.brand,
    },
    offers: {
      "@type": "Offer",
      url: product.url,
      priceCurrency: product.currency,
      price: product.price,
      itemCondition: "https://schema.org/NewCondition",
      availability: "https://schema.org/InStock",
    },
  }}
/>

<h1>{product.name}</h1>
<p>{product.description}</p>
