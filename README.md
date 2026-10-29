<p align="center">
  <img src="https://raw.githubusercontent.com/omkarcloud/botasaurus/master/images/mascot.png" alt="aliexpress scraper" />
</p>
<div align="center" style="margin-top: 0;">
  <h1>✨ AliExpress Scraper 🤖</h1>
  <p><strong>Scrape AliExpress product search, full product details, prices, SKU variants, customer reviews and Q&amp;A in real time — across 64 ship-to countries. Clean JSON, no blocks, no proxies.</strong></p>
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

AliExpress Scraper turns AliExpress into clean JSON, pulled live from the site — no blocks, no proxies to manage. Pull full product details — every SKU variant with its own price and stock, images, video, specifications, shipping estimates, and store info — search products with sorting and filters, and page through every customer review and every customer question with its answer — all via one API.

Prices come back numeric with the discount (and per-SKU pricing on product pages), so you can compare, monitor, and analyze prices programmatically instead of scraping HTML yourself.

It works across **64 ship-to countries** via `country_code` — results are localized and **prices come back in each country's own currency automatically**.

- **Rated Excellent — 4.7 based on 37 reviews** on [Trustpilot](https://www.trustpilot.com/review/omkar.cloud). Our open source work is sponsored by [1000+ devs on GitHub](https://github.com/sponsors/omkarcloud).

[![Try the AliExpress Scraper API in the live playground — free, no signup](https://img.shields.io/badge/%E2%96%B6%20Playground-Run%20a%20live%20request%2C%20free-brightgreen?style=for-the-badge)](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=badge)

[![Free Plan: 100 requests per month](https://img.shields.io/badge/Free%20tier-100%20requests%2Fmonth-blue?style=for-the-badge)](#pricing)

The same scraper is also available on **Apify** and **RapidAPI**:

[![Run on Apify](https://img.shields.io/badge/Run%20on-Apify-blue)](https://apify.com/omkar-cloud/aliexpress-scraper) [![Run on RapidAPI](https://img.shields.io/badge/Run%20on-RapidAPI-blue?logo=rapidapi)](https://rapidapi.com/OmkarCloud/api/aliexpress-scraper-api1)

## Example: AliExpress Product Data in One Request

One request to the product details API — here for a best-selling necklace:

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/product?product=3256809570114841
```

```json
{
  "id": "1005009756429593",
  "title": "A-Z Initial Necklace 18K Gold Plated Necklace Cute Letter Stainless Steel Necklace for Women",
  "link": "https://www.aliexpress.com/item/1005009756429593.html",
  "rating": 4.6,
  "reviews_count": 2165,
  "orders_count": 10000,
  "wishlist_count": 3628,
  "stock": 1004,
  "pricing": {"sale_price": 1.09, "original_price": 4.37, "discount_percent": 75, "currency": "USD"},
  "video": "https://video.aliexpress-media.com/play/u/ae_sg_item/3000923856025/p/1/e/6/t/10301/5000284426458.mp4",
  "sku_properties": [{ "name": "Metal Color", "values": [{"id": 361180, "name": "A"}, {"id": 17053024, "name": "C"}, {"id": 201447815, "name": "B"}, "…"] }],
  "skus": [
    { "id": "12000050070190057", "label": "D", "is_available": true, "stock": 57, "pricing": {"sale_price": 1.09, "original_price": 4.3, "discount_percent": 74, "currency": "USD"} },
    { "id": "12000050070190056", "label": "C", "is_available": true, "stock": 29, "pricing": {"sale_price": 1.09, "original_price": 4.3, "discount_percent": 74, "currency": "USD"} }
  ],
  "shipping": {
    "ship_to": "US",
    "options": [
      { "name": "AliExpress Selection Standard Shipping", "price": 1.99, "currency": "USD", "ship_from": "China", "min_delivery_days": 6, "max_delivery_days": 10, "has_tracking": true }
    ]
  },
  "store": { "name": "MECYLIFE Store", "positive_rate_percent": 93.7, "is_top_rated": false }
}
````

*Trimmed for readability — the full response also has all images, every SKU variant with its own price and stock, the full `sku_properties`, specifications, category, per-option shipping estimates with dates, and the store. See the [sample response](#product-details) in the API reference.*

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
  "count": 932,
  "per_page": 60,
  "current_page": 2,
  "total_pages": 16,
  "next": "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/v2/search?query=wireless%2520earbuds&page=3&sort_by=price_low_to_high&country_code=DE",
  "previous": "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/v2/search?query=wireless%2520earbuds&sort_by=price_low_to_high&country_code=DE",
  "currency": "EUR",
  "results": [
    {
      "id": "1005013054478555",
      "title": "F26E01 Wireless Bluetooth In-Ear Earbuds: Clear Sound, Built-In Mic, Premium Materials, Long Battery Life - Ideal for Travel, Office, and Gaming",
      "link": "https://www.aliexpress.us/item/1005013054478555.html",
      "image": "https://ae-pic-a1.aliexpress-media.com/kf/Sd009f21dc43f40d6a370aedd0693f969l.jpg",
      "images": [
        "https://ae-pic-a1.aliexpress-media.com/kf/Sd009f21dc43f40d6a370aedd0693f969l.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/Sb047726f813846eaaa2cbae42e804272u.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/Sc721a461275c4a20aeb667004b7393acx.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/Sa3012150e30e4e29838942c1170bae6bV.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/S8b9c3d0f88e644b4bcb255c720aec4033.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/S517b931e269c495fb704bf6abc4b52b9v.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/S2f04582a156b434182ba0e49e97b6ec1W.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/S8c716e4468644c088df453af67976fb1z.jpg"
      ],
      "rating": 4.0,
      "orders_count": 6,
      "is_hot_sale": null,
      "is_choice": false,
      "pricing": {
        "sale_price": 15.39,
        "original_price": null,
        "discount_percent": 25,
        "currency": "EUR",
        "tax_rate": 0.19,
        "sku_id": "12000060162104149"
      },
      "tags": [],
      "store_name": null,
      "category_ids": [
        44,
        100000306,
        63705
      ],
      "listed_date": "2026-08-27"
    }
  ]
}
````

</details>

---

### Product Details

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-product)

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/product?product=3256809570114841
```

Real-time full product details. `product` accepts a product URL or a numeric ID — both the `1005…` and `3256…` ID forms work for any country; conversion is automatic. Returns 404 if the product does not exist.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product` | Yes | — | Product URL or numeric product ID. |
| `country_code` | No | `US` | Ship-to country — prices (including per-SKU) come back in its currency. |

Returns the product's pricing with discount, every SKU variant with its own stock and pricing, `sku_properties`, images, video, specifications, rating/reviews/orders/wishlist counts, per-option shipping estimates, and store info.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "id": "1005009756429593",
  "canonical_id": "1005009756429593",
  "title": "A-Z Initial Necklace 18K Gold Plated Necklace Cute Letter Stainless Steel Necklace for Women",
  "link": "https://www.aliexpress.com/item/1005009756429593.html",
  "images": [
    "https://ae-pic-a1.aliexpress-media.com/kf/S9231a1e540d54ab9a0fa34603e6ca4988.jpg?has_lang=1&ver=2",
    "https://ae-pic-a1.aliexpress-media.com/kf/S41ec8ed3d92b4d3a8e2785e4576b5586O.jpg?has_lang=1&ver=2"
  ],
  "video": {
    "link": "https://video.aliexpress-media.com/play/u/ae_sg_item/3000923856025/p/1/e/6/t/10301/5000284426458.mp4",
    "thumbnail": "https://ae-pic-a1.aliexpress-media.com/kf/S58260c9ce8c047f1a393f9d5608465eeG.jpg"
  },
  "rating": 4.6,
  "reviews_count": 2165,
  "orders_count": 10000,
  "orders_label": "10,000+ sold",
  "wishlist_count": 3628,
  "stock": 1004,
  "max_per_buyer": 1,
  "pricing": {
    "sale_price": 1.09,
    "original_price": 4.37,
    "discount_percent": 75,
    "currency": "USD"
  },
  "coupons": [],
  "category": {
    "id": 200000162,
    "path": null
  },
  "sku_properties": [
    {
      "id": 200001034,
      "name": "Metal Color",
      "values": [
        {
          "id": 361180,
          "name": "A",
          "image": "https://ae-pic-a1.aliexpress-media.com/kf/S28f3e4546e934ef6bd5b630825300aebo.jpg_640x640.jpg_.webp"
        },
        {
          "id": 17053024,
          "name": "C",
          "image": "https://ae-pic-a1.aliexpress-media.com/kf/S32e2ce5c9fc34b928fc4dcb1091b2b23t.jpg_640x640.jpg_.webp"
        }
      ]
    }
  ],
  "skus": [
    {
      "id": "12000050070190057",
      "label": "D",
      "attributes": "200001034:201673808#D;200000639:200661028",
      "is_available": true,
      "stock": 57,
      "max_per_buyer": 1,
      "pricing": {
        "sale_price": 1.09,
        "original_price": 4.3,
        "discount_percent": 74,
        "currency": "USD"
      }
    },
    {
      "id": "12000050070190056",
      "label": "C",
      "attributes": "200001034:17053024#C;200000639:200661028",
      "is_available": true,
      "stock": 29,
      "max_per_buyer": 1,
      "pricing": {
        "sale_price": 1.09,
        "original_price": 4.3,
        "discount_percent": 74,
        "currency": "USD"
      }
    }
  ],
  "specifications": [
    {
      "name": "Certification",
      "value": "REACH"
    },
    {
      "name": "High-concerned chemical",
      "value": "none"
    }
  ],
  "shipping": {
    "ship_to": "US",
    "options": [
      {
        "code": "CAINIAO_FULFILLMENT_STD",
        "name": "AliExpress Selection Standard Shipping",
        "price": 1.99,
        "currency": "USD",
        "is_free": false,
        "ship_from": "China",
        "min_delivery_days": 6,
        "max_delivery_days": 10,
        "estimated_delivery_min_date": "2026-11-04",
        "estimated_delivery_max_date": "2026-11-08",
        "has_tracking": true,
        "guaranteed_delivery_days": 60,
        "is_selected": true
      }
    ]
  },
  "store": {
    "id": 1105052644,
    "name": "MECYLIFE Store",
    "link": "https://www.aliexpress.com/store/1105052644",
    "seller_id": 6003240024,
    "country": null,
    "province": null,
    "opened_date": null,
    "is_top_rated": false,
    "is_local_seller": false,
    "positive_rate_percent": 93.7,
    "positive_reviews_count": null,
    "reviews_count": null,
    "followers_count": null
  },
  "description_link": null,
  "description_json_link": "https://pdp.aliexpress-media.com/product/description/stdmobile/v2/en_US/desc.json?productId=1005009756429593&key=Sd4adf0814af74c0196408d4d494e4f79M.json&token=4bb7691d8e7fbef4723183b4039b8a4a&sellerId=6003240024"
}
````

</details>

---

### Product Reviews

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-reviews)

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/reviews?product=1005008320757869
```

Every customer review of a product, 20 per page with `next`/`previous` links, plus the star breakdown and — on page 1 — the tags buyers picked.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product` | Yes | — | Product URL or numeric product ID. |
| `page` | No | `1` | Page number, 20 reviews per page. |
| `filter` | No | `all` | `all`, `image` (with photos), `local` (shopper's country), `additional` (with a follow-up), or a star level `1`–`5`. |
| `country_code` | No | `US` | Picks the `local` filter's country and the translation language. |

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "count": 291,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 15,
  "next": "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/v2/reviews?product=1005008320757869&filter=image&country_code=US&page=2",
  "previous": null,
  "statistics": {
    "average_rating": 4.8,
    "total_reviews": 1105,
    "positive_rate_percent": 96.7,
    "five_star": 979,
    "four_star": 90,
    "three_star": 15,
    "two_star": 7,
    "one_star": 14,
    "impressions": [
      {
        "text": "cute design",
        "count": 269,
        "is_positive": true
      },
      {
        "text": "perfect fit",
        "count": 75,
        "is_positive": true
      },
      {
        "text": "nice quality",
        "count": 54,
        "is_positive": true
      }
    ]
  },
  "results": [
    {
      "id": "60096731722701860",
      "rating": 5.0,
      "author": "0***r",
      "country": "US",
      "date": "2026-05-13",
      "text": "Shipped very fast! And the case is very cute, arrived in mint condition. If you’re looking for something that will protect your phone long term, this is unfortunately not the case because it is made of silicone or a silicone like material as shown in the images but very cute for photo shoots or going out and I still 100% recommend. One small complaint is that it has some fitting issues on the top of my phone and camera. Also this made me realize actually how badly I needed to clean my phone without the case, GUYS CLEAN YOUR DEVICES!! I 100% recommend buying for decorative purposes 🙂",
      "translated_text": null,
      "sku": "Color:Pink Compatible-Phone Models:iPhone 11",
      "images": [
        "https://ae-pic-a1.aliexpress-media.com/kf/A287caf80f6fb4e07885baf3f0e70b967F.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/A6ab6f10fd45740fc93eab8c5893c6275k.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/A24128d6eea684017b52a8ac5337d24d4a.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/A560965e25ee24287b4b59c17234007eaT.jpg",
        "https://ae-pic-a1.aliexpress-media.com/kf/Ab81f548425104f0e81917957f60ac4a1S.jpg"
      ],
      "thumbnails": [
        "http://ae-pic-a1.aliexpress-media.com/kf/A287caf80f6fb4e07885baf3f0e70b967F.jpg_220x220.jpg",
        "http://ae-pic-a1.aliexpress-media.com/kf/A6ab6f10fd45740fc93eab8c5893c6275k.jpg_220x220.jpg",
        "http://ae-pic-a1.aliexpress-media.com/kf/A24128d6eea684017b52a8ac5337d24d4a.jpg_220x220.jpg",
        "http://ae-pic-a1.aliexpress-media.com/kf/A560965e25ee24287b4b59c17234007eaT.jpg_220x220.jpg",
        "http://ae-pic-a1.aliexpress-media.com/kf/Ab81f548425104f0e81917957f60ac4a1S.jpg_220x220.jpg"
      ],
      "upvotes": 4,
      "downvotes": 0,
      "is_anonymous": false,
      "additional_feedback": null,
      "logistics": "AliExpress Selection Standard Shipping"
    }
  ]
}
```

</details>

---

### Product Questions

▶ [Try it live in the Playground →](https://www.omkar.cloud/tools/aliexpress-scraper-api/playground?utm_source=github&utm_medium=cpc&utm_content=endpoint-questions)

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress/v2/questions?product=3256804853498073
```

The product's customer Q&A, 20 per page: each question with the asker, date, number of answers and the top answer, with translations.

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product` | Yes | — | Product URL or numeric product ID. |
| `page` | No | `1` | Page number, 20 questions per page. |
| `country_code` | No | `US` | Translation language of questions and answers. |

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "count": 68,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 4,
  "next": "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/v2/questions?product=3256804853498073&country_code=US&page=2",
  "previous": null,
  "total_answers": 31,
  "results": [
    {
      "id": "120000020617248",
      "question": "does it come with retail packing",
      "translated_question": null,
      "language": "en",
      "asked_date": "2026-10-11",
      "asker": {
        "name": "G***n",
        "country": "CA"
      },
      "answers_count": 1,
      "answer": {
        "text": "Yes",
        "translated_text": null,
        "language": "nl",
        "date": "2026-10-13",
        "author": "J***d",
        "country": "NL",
        "is_purchaser": true
      }
    }
  ]
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
| Free | $0 | 100 |
| Starter | $16 | 3,000 |
| Grow | $48 | 15,000 |
| Scale | $148 | 75,000 |

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

### Can I get a product's reviews and Q&A?

Yes. Product Reviews pages through every review (20 per page) with the rating, text and translation, photos and votes — filter to photo reviews, the shopper's country or one star level — and returns the star breakdown plus the tags buyers picked. Product Questions returns the customer Q&A with the top answer to each question.

### Will I get blocked or need proxies?

No. We handle the scraping infrastructure — you call a normal REST API and never touch AliExpress directly, so there are no proxies, headless browsers, or CAPTCHAs on your side.

### Can I pass a product URL instead of an ID?

Yes. Product Details, Reviews and Questions accept a full item URL or a bare numeric ID, and both the `1005…` and `3256…` ID forms work for any country — conversion is automatic.

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
