# Sveltekit-Seo-Enhancer

Enhance SEO capabilities in your SvelteKit applications with ease. This component simplifies the management of meta tags,
structured data, and other SEO-related elements dynamically.

# Features

- Dynamic Meta Tags: Set and update meta tags (like title, description) based on page content dynamically.
- Structured Data (JSON-LD): Easily integrate structured data for better search engine understanding.
- Flexible Configuration: Customize meta tags, links, scripts, and structured data per page or component.
- Lifecycle Management: Automatically updates meta tags on component mount and manages cleanup on component unmount.

# Installation

Install the package using npm:

```bash
npm install sveltekit-seo-enhancer
```

# Usage

Basic Example
Import and use the 'SeoEnhancer' component in your SvelteKit pages or components:

```bash
<script>
  import SeoEnhancer from 'sveltekit-seo-enhancer';

  let product = {
    name: 'Awesome Product',
    description: 'This is an awesome product.',
    url: 'https://www.example.com/product/awesome',
    imageUrl: 'https://www.example.com/product/awesome.jpg',
    price: '119.99',
    currency: 'USD',
    brand: 'ACME'
  };

  let metaTags = [
    { name: "description", content: product.description },
    { property: "og:title", content: product.name },
    { property: "og:description", content: product.description },
    { property: "og:url", content: product.url },
    { property: "og:image", content: product.imageUrl }
  ];
</script>

<SeoEnhancer
  title={product.name}
  meta={metaTags}
  link={[
    { rel: 'canonical', href: product.url }
  ]}
  jsonld={{
    "@context": "https://schema.org",
    "@type": "Product",
    "name": product.name,
    "image": product.imageUrl,
    "description": product.description,
    "sku": "0446310786",
    "brand": {
      "@type": "Brand",
      "name": product.brand
    },
    "offers": {
      "@type": "Offer",
      "url": product.url,
      "priceCurrency": product.currency,
      "price": product.price,
      "itemCondition": "https://schema.org/NewCondition",
      "availability": "https://schema.org/InStock"
    }
  }}
/>
```

# Contributions

Contributions are welcome! Please fork the repository and submit a pull request with your enhancements.

# License

This project is licensed under the MIT License.

# Acknowledgements

Inspiration and guidance from Sveltekit Docs and Best SEO Practices.

### Summary

1. **Use** the `SeoEnhancer` component in your default `+page.svelte`.
2. **Configure** your `package.json` with the necessary fields and scripts.
3. **Build** the project using the configured build script.
4. **Publish** the package to npm.
5. **Include** a comprehensive `README.md` to guide users on installation and usage.

By following these steps, you can ensure your SvelteKit component is ready for use and easily integrable by others.
