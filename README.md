![AliExpress Scraper Featured Image](https://raw.githubusercontent.com/omkarcloud/aliexpress-scraper/master/aliexpress-scraper-featured-image.png)

# AliExpress Scraper API

Search products, get variant-level pricing, HD images, seller info, and stock quantities from AliExpress — one API call, clean JSON. 5,000 free requests/month.

## Key Features

- Search AliExpress products by keyword
- Get full product details — pricing per variant, HD images, seller info, package dimensions
- Paginated search with 40K+ results per query
- **5,000 requests/month on free tier**
- Example Response:
```json
{
  "id": "1005007170995524",
  "title": "Earbuds True Wireless Earphone Noise Cancelling Update Bluetooth 5.3 Headset HD Music Headphone In-Ear Handsfree With Mic",
  "image_url": "https://ae01.alicdn.com/kf/S932a8a2d640f4b0d9ca435c91c870edb3.jpg",
  "price": "5.43",
  "original_price": "5.66",
  "currency": "USD",
  "discount": "4%",
  "rating": 4.9,
  "positive_feedback_rate": "98.0",
  "orders_count": 321,
  "category_ids": "44,100000306,63705"
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key.

It takes just 2 minutes to sign up. You get 5,000 free requests every month for detailed AliExpress data — more than enough for most users to get their job done without paying a dime.

This is a well built product, and your search for the best AliExpress Scraper API ends right here.


## Quick Start

```bash
curl -X GET "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search?query=wireless%20earbuds" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
  "results": [
    {
      "id": "1005007170995524",
      "title": "Earbuds True Wireless Earphone Noise Cancelling Update Bluetooth 5.3 Headset HD Music Headphone In-Ear Handsfree With Mic",
      "image_url": "https://ae01.alicdn.com/kf/S932a8a2d640f4b0d9ca435c91c870edb3.jpg",
      "price": "5.43",
      "original_price": "5.66",
      "currency": "USD",
      "discount": "4%",
      "rating": 4.9,
      "positive_feedback_rate": "98.0",
      "orders_count": 321,
      "category_ids": "44,100000306,63705"
    }
  ]
}
```

## Quick Start (Python)

```bash
pip install requests
```

```python
import requests

# Search for products
response = requests.get(
    "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search",
    params={"query": "wireless earbuds"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```


## API Reference

### Product Search

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `query` | Yes | — | Keyword or phrase to search for. |
| `page` | No | `1` | Page number. |

#### Example

```python
import requests

response = requests.get(
    "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search",
    params={"query": "wireless earbuds"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "count": 40100,
  "per_page": 20,
  "current_page": 1,
  "total_pages": 2005,
  "next": "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search?query=wireless+earbuds&page=2",
  "previous": null,
  "results": [
    {
      "id": "1005007170995524",
      "title": "Earbuds True Wireless Earphone Noise Cancelling Update Bluetooth 5.3 Headset HD Music Headphone In-Ear Handsfree With Mic",
      "image_url": "https://ae01.alicdn.com/kf/S932a8a2d640f4b0d9ca435c91c870edb3.jpg",
      "price": "5.43",
      "original_price": "5.66",
      "currency": "USD",
      "discount": "4%",
      "rating": 4.9,
      "positive_feedback_rate": "98.0",
      "orders_count": 321,
      "category_ids": "44,100000306,63705"
    },
    {
      "id": "1005008481982828",
      "title": "A99E-Earbuds,Over The Ear Earbuds Earbuds True Wireless Open Ear Earbuds Bluetooth 5.4, Ipx5 Earbuds Noise Cancellation",
      "image_url": "https://ae01.alicdn.com/kf/S50223ba5440341258f89534c4a5e06a9d.jpg",
      "price": "26.03",
      "original_price": "24.65",
      "currency": "USD",
      "discount": "0%",
      "rating": null,
      "positive_feedback_rate": "",
      "orders_count": null,
      "category_ids": "44,100000306,63705"
    }
  ]
}
```

</details>

---

### Product Details

```
GET https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/product
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product_id` | Yes | — | AliExpress product ID (e.g., `1005007170995524`). |

#### Example

```python
import requests

response = requests.get(
    "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/product",
    params={"product_id": "1005007170995524"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response Fields

Returns product title, category, listing URL, all images (standard + HD), video URL, package dimensions, currency info, full variant breakdown with images, per-SKU pricing (list price, sale price, discount, stock), and seller details.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "id": "1005007170995524",
  "title": "Earbuds True Wireless Earphone Noise Cancelling Update Bluetooth 5.3 Headset HD Music Headphone In-Ear Handsfree With Mic",
  "category_id": 63705,
  "listing_url": "https://ar.aliexpress.com/item/1005007170995524.html",
  "images": [
    "https://ae01.alicdn.com/kf/S408f97b7af7b4c54bc04c46285559f704.jpg",
    "https://ae01.alicdn.com/kf/Sd9ea2a5491f24a759d6d43e545fbd30di.jpg",
    "https://ae01.alicdn.com/kf/S3cc9aaf17a3640e68681d32c7d2c10609.jpg",
    "https://ae01.alicdn.com/kf/Sa17a49b1fdab42e9976201fb9955c098L.jpg",
    "https://ae01.alicdn.com/kf/S24a669a4c83442819e43b437b2bf3c60T.jpg",
    "https://ae01.alicdn.com/kf/Se0a77bc7d00e4fef8145fb984786c300x.jpg"
  ],
  "images_hd": [
    "https://ae01.alicdn.com/kf/S408f97b7af7b4c54bc04c46285559f704.jpg",
    "https://ae01.alicdn.com/kf/Sd9ea2a5491f24a759d6d43e545fbd30di.jpg",
    "https://ae01.alicdn.com/kf/S3cc9aaf17a3640e68681d32c7d2c10609.jpg",
    "https://ae01.alicdn.com/kf/Sa17a49b1fdab42e9976201fb9955c098L.jpg",
    "https://ae01.alicdn.com/kf/S24a669a4c83442819e43b437b2bf3c60T.jpg",
    "https://ae01.alicdn.com/kf/Se0a77bc7d00e4fef8145fb984786c300x.jpg"
  ],
  "video_url": null,
  "package": {
    "length_cm": 14,
    "width_cm": 10,
    "height_cm": 8,
    "weight_kg": 0.093
  },
  "currency": "USD",
  "base_currency": "CNY",
  "variants": [
    {
      "attribute_name": "Color",
      "attribute_id": "14",
      "has_color": true,
      "is_size": false,
      "options": [
        {
          "value_id": 193,
          "name": "black",
          "image_url": "https://ae01.alicdn.com/kf/S932a8a2d640f4b0d9ca435c91c870edb3.jpg",
          "thumbnail_url": "https://ae01.alicdn.com/kf/S932a8a2d640f4b0d9ca435c91c870edb3.jpg_120x120.jpg"
        }
      ]
    }
  ],
  "sku_pricing": [
    {
      "sku_id": "12000039691611222",
      "variant_ids": "193",
      "list_price": 9.94,
      "sale_price": 4.57,
      "formatted_sale_price": "US $4.57",
      "discount_label": "54% off",
      "available_quantity": 5
    }
  ],
  "seller": {
    "name": "Stone's Store",
    "id": "1103576287",
    "logo_url": "https://ae01.alicdn.com/kf/Se90fceedf9d34ad1a8979283c98a1e45I/144x144.png"
  },
  "has_welcome_deal": false
}
```

</details>

## Error Handling

```python
response = requests.get(
    "https://aliexpress-scraper-api.omkar.cloud/aliexpress-scraper/search",
    params={"query": "wireless earbuds"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## FAQs

### What data does the API return?

**Product Search** returns per product: product ID, title, image URL, sale price, original price, currency, discount, star rating, positive feedback rate, order count, and category IDs.

**Product Details** returns: product ID, title, category ID, listing URL, all product images (standard + HD), video URL, package dimensions (length, width, height, weight), currency info, full variant breakdown (color, size, etc.) with images per option, per-SKU pricing (list price, sale price, discount label, stock quantity), and seller name, ID, and logo.

All in structured JSON. Ready to use in your app.

### How accurate is the data?

Data is pulled from AliExpress in real time. Every API call fetches live data — not cached or stale results. Prices, variants, stock levels, and seller info reflect what's on AliExpress right now.

### Where do I find the product ID?

The product ID is in any AliExpress product URL. For example:

`https://www.aliexpress.com/item/1005007170995524.html` → product ID is `1005007170995524`

You can also get product IDs from the Product Search endpoint results.

### Does it return variant-level pricing?

Yes. The Product Details endpoint returns pricing for every SKU variant — sale price, list price, discount percentage, and available stock. Each SKU maps to specific variant options (e.g., "Color: black").

### Can I use this for dropshipping?

Absolutely. The API gives you everything a dropshipping tool needs: product titles, images, variant-level pricing, stock quantities, package dimensions for shipping estimates, and seller info.

### Does the search support pagination?

Yes. Pass the `page` parameter to paginate through results. The response includes `count`, `total_pages`, and ready-to-use `next`/`previous` links.

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about AliExpress Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20AliExpress%20Scraper%20API.)

[![Contact Us on Email about AliExpress Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=AliExpress%20Scraper%20API%20Question)
