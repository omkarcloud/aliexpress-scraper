<p align="center">
  <img src="https://raw.githubusercontent.com/omkarcloud/botasaurus/master/images/mascot.png" alt="aliexpress scraper" />
</p>
<div align="center" style="margin-top: 0;">
  <h1>✨ AliExpress Scraper 🤖</h1>
  <p><strong>Scrape AliExpress product search, prices, SKU variants, ratings, orders, and shipping in real time — across 64 ship-to countries. Clean JSON, no blocks, no proxies.</strong></p>
</div>
<em>
  <h5 align="center">(Programming Language - Python 3)</h5>
</em>
<p align="center">
  <a href="#">
    <img alt="aliexpress-scraper forks" src="https://img.shields.io/github/forks/omkarcloud/aliexpress-scraper?style=for-the-badge" />
  </a>
  <a href="#">
    <img alt="Repo stars" src="https://img.shields.io/github/stars/omkarcloud/aliexpress-scraper?style=for-the-badge&color=yellow" />
  </a>
</p>
<p align="center">
  <img src="https://views.whatilearened.today/views/github/omkarcloud/aliexpress-scraper.svg" width="80px" height="28px" alt="View" />
</p>

AliExpress Scraper turns AliExpress into clean JSON, pulled live from the site — no blocks, no proxies to manage. Search products with sorting and filters, and pull full product details — every SKU variant with its own price and stock, images, specifications, shipping estimates, and store info — all via one API.

Prices come back numeric with the discount (and per-SKU pricing on product pages), so you can compare, monitor, and analyze prices programmatically instead of scraping HTML yourself.

It works across **64 ship-to countries** via `country_code` — results are localized and **prices come back in each country's own currency automatically** (US requests are served from aliexpress.us, all other countries from aliexpress.com).

- **Rated Excellent — 4.6 based on 25 reviews** on [Trustpilot](https://www.trustpilot.com/review/omkar.cloud). Our open source work is sponsored by [1000+ devs on GitHub](https://github.com/sponsors/omkarcloud).

[![Try the AliExpress Scraper API in the live playground — free, no signup](https://img.shields.io/badge/%E2%96%B6%20Playground-Run%20a%20live%20request%2C%20free-brightgreen?style=for-the-badge)](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=badge)

[![Free Plan: 200 requests per month](https://img.shields.io/badge/Free%20tier-200%20requests%2Fmonth-blue?style=for-the-badge)](#pricing)

The same scraper is also available on **Apify** and **RapidAPI**:

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-blue)](https://apify.com/omkar-cloud/aliexpress-scraper) [![Run on RapidAPI](https://img.shields.io/badge/Run%20on-RapidAPI-blue?logo=rapidapi)](https://rapidapi.com/OmkarCloud/api/aliexpress-scraper-api1)

## Example: AliExpress Product Data in One Request

One request to the product details API:

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/product?product=3256810554614749
```

```json
{
  "id": "3256810554614749",
  "canonical_id": "3256810554614749",
  "title": "Joyfy Rubber Ducks Random Assortment Mini Rubber Duckie Toys for Kids Bath Shower Toys Birthday Gifts Summer Beach Pool Activity",
  "link": "https://www.aliexpress.com/item/3256810554614749.html",
  "rating": 4.9,
  "reviews_count": 56,
  "orders_count": 474,
  "wishlist_count": 116,
  "stock": 492,
  "pricing": {
    "sale_price": 0.99,
    "original_price": 19.06,
    "discount_percent": 95,
    "currency": "USD"
  },
  "coupons": ["$2.00 off on $18.00"],
  "skus": [
    {
      "id": "12000055944024788",
      "label": "15pc",
      "is_available": true,
      "stock": 158,
      "pricing": { "sale_price": 0.99, "original_price": 19.06, "discount_percent": 95, "currency": "USD" }
    },
    {
      "id": "12000055944024790",
      "label": "30pcs",
      "is_available": true,
      "stock": 127,
      "pricing": { "sale_price": 7.12, "original_price": 33.94, "discount_percent": 79, "currency": "USD" }
    }
  ],
  "shipping": {
    "ship_to": "US",
    "options": [
      {
        "name": "AE_US_SAVER",
        "is_free": true,
        "ship_from": "United States",
        "min_delivery_days": 3,
        "max_delivery_days": 9,
        "estimated_delivery_max_date": "2026-08-11",
        "has_tracking": true
      }
    ]
  },
  "store": {
    "id": 1105246100,
    "name": "Shop1105233629 Store",
    "link": "https://www.aliexpress.com/store/1105246100",
    "country": "China",
    "followers_count": 61
  }
}
```

*Trimmed for readability — the full response also has all product images, video, every SKU variant with its own price and stock, `sku_properties`, specifications, coupons, category path, per-option shipping estimates, full store stats, and the description links. See the [sample response](#product-details) in the API reference.*

Add `country_code` to localize the product to any of 64 countries — prices come back in that country's currency automatically.

**[Run this exact request in the Playground — no signup, no key →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=example)**

The playground comes prefilled with this request and runs it against the live API in your browser. The JSON it returns is identical to what the API returns.

## Start Getting Data in Minutes

Python and Node.js integration examples are available for every endpoint in the playground, so you can get AliExpress data in minutes instead of days.

```python
import requests

# Scrape AliExpress product search results, live
response = requests.get(
    "https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/search",
    params={"query": "rubber duck", "sort_by": "most_orders", "country_code": "US"},
    headers={"API-Key": "YOUR_API_KEY"},
)

print(response.json())
```

## API Reference

All endpoints are GET requests against `https://aliexpress-scraper-api.omkar.cloud`, authenticated with the `API-Key` header, returning JSON.

Add `country_code` to any request to localize results to one of [64 ship-to countries](#supported-countries) — **prices come back in that country's currency automatically**.

### Product Search

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-search)

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/search?query=rubber+duck
```

Real-time AliExpress product search with sorting and filters. Returns 60 products per page with `next`/`previous` pagination links.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `query` | Yes | — | Keyword or phrase to search for (e.g. `raspberry pi`). |
| `page` | No | `1` | Page number, 60 products per page. |
| `country_code` | No | `US` | Ship-to country — localizes results and returns prices in its currency. |
| `sort_by` | No | `best_match` | `best_match`, `most_orders`, `price_low_to_high`, `price_high_to_low`. |
| `min_price` / `max_price` | No | — | Price range, in the selected country's currency. |
| `free_shipping` | No | `false` | Only products with free shipping. |
| `savings` | No | `false` | Only products with savings/discount deals. |
| `four_star_and_up` | No | `false` | Only products rated 4 stars and above. |
| `choice` | No | `false` | Only AliExpress Choice products. |

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "count": 12017,
  "per_page": 60,
  "current_page": 1,
  "total_pages": 201,
  "next": "https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/search?query=rubber+duck&page=2",
  "previous": null,
  "currency": "USD",
  "results": [
    {
      "id": "3256810554614749",
      "title": "Joyfy Rubber Ducks Random Assortment Mini Rubber Duckie Toys for Kids Bath Shower Toys Birthday Gifts Summer Beach Pool Activity",
      "link": "https://www.aliexpress.us/item/3256810554614749.html",
      "image": "https://ae-pic-a1.aliexpress-media.com/kf/Sf1ea8500f8bb4e37b31702f533e083a8v.jpg",
      "images": [
        "https://ae-pic-a1.aliexpress-media.com/kf/Sf1ea8500f8bb4e37b31702f533e083a8v.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/S3f715f2a467142728261a755015531703.jpg"
      ],
      "rating": 4.9,
      "orders_count": 474,
      "is_hot_sale": false,
      "is_choice": false,
      "pricing": {
        "sale_price": 0.99,
        "original_price": 19.06,
        "discount_percent": 94,
        "currency": "USD",
        "tax_rate": 0,
        "sku_id": "12000055944024788"
      },
      "tags": ["New shoppers save $18.07", "Extra 2% off with coins"],
      "store_name": "Shop1105233629 Store",
      "category_ids": [26, 200389159, 100001766],
      "listed_date": "2026-01-07"
    }
  ]
}
```

</details>

---

### Product Details

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-product)

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/product?product=3256810554614749
```

Real-time full product details. `product` accepts a product URL or a numeric ID — both the `1005…` (aliexpress.com) and `3256…` (aliexpress.us) ID forms work for any country; conversion is automatic. Returns 404 if the product does not exist.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product` | Yes | — | Product URL or numeric product ID. |
| `country_code` | No | `US` | Ship-to country — prices (including per-SKU) come back in its currency. |

Returns the product's pricing with discount, every SKU variant with its own stock and pricing, `sku_properties`, images, video, specifications, coupons, category path, rating/reviews/orders/wishlist counts, per-option shipping estimates, and full store info.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "id": "3256810554614749",
  "canonical_id": "3256810554614749",
  "title": "Joyfy Rubber Ducks Random Assortment Mini Rubber Duckie Toys for Kids Bath Shower Toys Birthday Gifts Summer Beach Pool Activity",
  "link": "https://www.aliexpress.com/item/3256810554614749.html",
  "images": [
    "https://ae-pic-a1.aliexpress-media.com/kf/Sf1ea8500f8bb4e37b31702f533e083a8v.jpg?has_lang=1&ver=1",
    "https://ae-pic-a1.aliexpress-media.com/kf/S3f715f2a467142728261a755015531703.jpg"
  ],
  "video": null,
  "rating": 4.9,
  "reviews_count": 56,
  "orders_count": 474,
  "orders_label": "This seller: 474 sales | Total sales: 474",
  "wishlist_count": 116,
  "stock": 492,
  "max_per_buyer": 1,
  "pricing": { "sale_price": 0.99, "original_price": 19.06, "discount_percent": 95, "currency": "USD" },
  "coupons": ["$2.00 off on $18.00"],
  "category": { "id": 100001766, "path": "26/200389159/100001766" },
  "sku_properties": [
    {
      "id": 14,
      "name": "Color",
      "values": [
        { "id": 29, "name": "15pc", "image": null },
        { "id": 193, "name": "30pcs", "image": null }
      ]
    }
  ],
  "skus": [
    {
      "id": "12000055944024788",
      "label": "15pc",
      "attributes": "200007763:201336106;14:29#15pc",
      "is_available": true,
      "stock": 158,
      "max_per_buyer": 1,
      "pricing": { "sale_price": 0.99, "original_price": 19.06, "discount_percent": 95, "currency": "USD" }
    },
    {
      "id": "12000055944024790",
      "label": "30pcs",
      "attributes": "200007763:201336106;14:193#30pcs",
      "is_available": true,
      "stock": 127,
      "max_per_buyer": 1,
      "pricing": { "sale_price": 7.12, "original_price": 33.94, "discount_percent": 79, "currency": "USD" }
    }
  ],
  "specifications": [
    { "name": "Material", "value": "Plastic" },
    { "name": "Brand Name", "value": "Joyfy" },
    { "name": "Recommend Age", "value": "3-6Y,6-12Y" }
  ],
  "shipping": {
    "ship_to": "US",
    "options": [
      {
        "code": "AE_US_SAVER",
        "name": "AE_US_SAVER",
        "price": null,
        "currency": "USD",
        "is_free": true,
        "ship_from": "United States",
        "min_delivery_days": 3,
        "max_delivery_days": 9,
        "estimated_delivery_min_date": "2026-08-05",
        "estimated_delivery_max_date": "2026-08-11",
        "has_tracking": true,
        "is_selected": true
      }
    ]
  },
  "store": {
    "id": 1105246100,
    "name": "Shop1105233629 Store",
    "link": "https://www.aliexpress.com/store/1105246100",
    "seller_id": 6003897797,
    "country": "China",
    "opened_date": "2025-11-24",
    "is_top_rated": false,
    "followers_count": 61
  }
}
```

</details>

---

### Supported Countries

Add `country_code` to any request to localize results and return prices in that country's currency. 64 ship-to countries are supported:

`US`, `UK`/`GB`, `DE`, `FR`, `ES`, `IT`, `NL`, `BE`, `PT`, `IE`, `AT`, `CH`, `SE`, `NO`, `DK`, `FI`, `PL`, `CZ`, `SK`, `HU`, `RO`, `BG`, `GR`, `HR`, `SI`, `LT`, `LV`, `EE`, `UA`, `TR`, `CA`, `MX`, `BR`, `AR`, `CL`, `CO`, `PE`, `IL`, `SA`, `AE`, `QA`, `KW`, `BH`, `OM`, `JO`, `EG`, `MA`, `DZ`, `TN`, `KE`, `JP`, `KR`, `SG`, `MY`, `TH`, `VN`, `PH`, `ID`, `IN`, `PK`, `BD`, `LK`, `AU`, `NZ`

## Pricing

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 200 |
| Starter | $16 | 20,000 |
| Grow | $48 | 100,000 |
| Scale | $148 | 400,000 |

1 API call = 1 request

Free Plan Available — [create your API key →](https://www.omkar.cloud/auth/sign-up?redirect=/api-key&utm_source=github&utm_medium=cpc&utm_content=pricing-signup). No credit card for the free tier.

## FAQs

### Can I try the API before signing up?

Yes. The playground runs live requests in your browser — free, no account, no API key. [Try it in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=faq)

### How do I search AliExpress products?

Call Product Search (`GET /aliexpress/v2/search?query=rubber+duck`) with a keyword. It returns 60 products per page — id, title, link, images, rating, order count, and pricing with discount — plus a `next` link to walk through every page. Refine with `sort_by`, `min_price`/`max_price`, `free_shipping`, `savings`, `four_star_and_up`, and `choice`.

### Do I get every SKU variant and its price?

Yes. Product Details returns each SKU variant with its own `stock` and `pricing` (sale price, original price, discount), plus `sku_properties` describing the options (color, size, ships-from). Perfect for price monitoring and building product catalogs.

### Does it work outside the US, in local currency?

Yes. Pass `country_code` — 64 ship-to countries are supported (`GB`, `DE`, `FR`, `BR`, `JP`, `IN`, `AU`, and more). Results are localized and prices come back in that country's own currency automatically.

### How fresh is the data?

Data is scraped from AliExpress in real time. Every API call fetches live data — not cached or stale results. Prices, stock, ratings, and order counts reflect what's on AliExpress right now.

### Will I get blocked or need proxies?

No. We handle the scraping infrastructure — you call a normal REST API and never touch AliExpress directly, so there are no proxies, headless browsers, or CAPTCHAs on your side.

### Can I pass a product URL instead of an ID?

Yes. Product Details accepts a full item URL or a bare numeric ID, and both the `1005…` (aliexpress.com) and `3256…` (aliexpress.us) ID forms work for any country — conversion is automatic.

## More E-commerce & Data Scrapers: Amazon & Google Maps

- **[Amazon Scraper API](https://github.com/omkarcloud/amazon-scraper)** — the same clean JSON for Amazon: product search, full product details, category browsing, and top reviews across 24 marketplaces. Compare the same product's price on AliExpress and Amazon.

- **[Google Maps Scraper (3,100+ GitHub Stars)](https://github.com/omkarcloud/google-maps-scraper)** — need tens of thousands of leads? Type a niche and a city ("dentists in New York") and get every matching business as a ready-to-call lead list — name, address, phone, website, emails, rating, and reviews. The free tier alone pulls up to 100K leads a month.

- **[Website Email Contact Scraper](https://github.com/omkarcloud/website-email-contact-scraper)** — **Free and open source.** Point it at any website and get every email, phone number, and social profile on it, each with source pages and an official/unofficial flag.

## Support

Built by developers, for developers — when you reach out, you talk to the engineers who built the API, not a support script. Message us anytime and we'll solve your query within 1 working day.


[![Contact Us on WhatsApp about AliExpress Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20AliExpress%20Scraper%20API.)

Email: [happy.to.help@omkar.cloud](mailto:happy.to.help@omkar.cloud?subject=AliExpress%20Scraper%20API%20Question)

[![Email Us about AliExpress Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=AliExpress%20Scraper%20API%20Question)

## Love It? Star It! ⭐

From one developer to another: If the AliExpress Scraper API saved you time, please [star the repo](https://github.com/omkarcloud/aliexpress-scraper).

Here's why it matters: most developers judge a scraper by its stars before trying it. Your star helps the next developer — someone deciding whether the AliExpress data here is real and reliable — try it with confidence.

It takes only 1 second, and means the world to me.
