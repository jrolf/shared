mercanto_share.md
---


## An Explanation of fields in the JSON schema:

---

### Top-Level Fields

1. **`product_id`**:
   - A unique identifier for the product.
   - Ensures that every product can be uniquely referenced in the system.

2. **`sku`**:
   - Stock Keeping Unit (SKU) identifier for the product.
   - Useful for managing inventory and integrating with external systems.

3. **`vendor`**:
   - Captures information about the vendor providing the product.
     - **`vendor_id`**: A unique identifier for the vendor.
     - **`vendor_product_id`**: Vendor-specific identifier for the product, if applicable.
     - **`vendor_name`**: The name of the vendor supplying the product.

4. **`product_name`**:
   - The full, official name of the product used in listings and displays.

5. **`short_name`**:
   - A simplified or alternative name for the product.
   - Useful for internal references or abbreviated views.

6. **`brand`**:
   - The brand associated with the product (e.g., "Coca-Cola", "Apple").
   - Helps in organizing and filtering products by brand.

7. **`description`**:
   - A concise description of the product, typically one to three sentences.
   - Highlights key details and characteristics.

8. **`long_product_desc`**:
   - A detailed, extended description of the product.
   - Includes rich details such as benefits, use cases, background information, and marketing copy.
   - Useful for SEO and user engagement.

9. **`image_url`**:
   - URL linking to an image of the product.
   - Enhances the visual appeal of listings and helps users identify the product quickly.

---

### Unit Details

10. **`unit_details`**:
    - Provides detailed information about the unit of measurement or packaging for the product.
      - **`unit_type`**: Specifies how the product is sold (e.g., "granel" for bulk, "pieza" for individual items, or "pieza_variable" for items sold by variable weight or size).
      - **`unit_size`**: Describes the size or weight of the unit (e.g., "1kg", "500ml").
      - **`unit_presentation`**: The packaging or format for the product units (e.g., "Caja", "Paquete").

---

### Pricing

11. **`pricing`**:
    - Contains information about product prices, including base price and bulk pricing.
      - **`base_price`**: The standard price of the product, including all applicable taxes.
      - **`bulk_quantity`**: The quantity threshold required to qualify for bulk pricing.
      - **`bulk_price`**: The discounted price for the bulk quantity, also including taxes.

---

### Taxes

12. **`taxes`**:
    - Captures tax-related details for the product.
      - **`IVA`**: Indicates if VAT (Value Added Tax) applies (`true` or `false`).
      - **`IEPS`**: Indicates if IEPS (a specific Mexican tax on certain goods) applies (`true` or `false`).
      - **`IEPS_rate`**: The applicable IEPS tax rate (decimal value, e.g., `0.08` for 8%).

---

### Classification

13. **`classification`**:
    - Describes the product's category and additional classification information.
      - **`category`**: The main category for the product (e.g., "Beverages", "Electronics").
      - **`subcategories`**: Additional subcategories or labels to provide more granular classification.

14. **`product_tags`**:
    - A list of non-hierarchical tags that describe the product’s attributes.
    - Tags are useful for search and filtering.
    - Examples: `["eco-friendly", "gluten-free", "sustainable"]`.

15. **`product_categories`**:
    - A hierarchical and mutually exclusive categorization of the product.
    - Helps structure products into distinct navigation paths.
    - Example: `["Food", "Beverages", "Juices"]`.

---

### Inventory

16. **`inventory`**:
    - Provides details about the availability and online integrations for the product.
      - **`available`**: A boolean indicating whether the product is currently in stock.
      - **`shopify_ids`**: An array of Shopify Collection IDs associated with the product (if applicable).

---

### Metadata

17. **`metadata`**:
    - Captures additional metadata for the product to enhance traceability, searchability, and system integration.
      - **`keywords`**: A list of keywords associated with the product to improve search engine performance and NLP-based search.
      - **`language`**: The language of the product description (e.g., "en", "es").
      - **`created_at`**: A timestamp recording when the product entry was created.
      - **`last_updated`**: A timestamp recording the most recent update to the product entry.

---

### Required Fields

- The following fields are **required** to ensure a consistent and functional representation of the product:
  - `product_id`
  - `product_name`
  - `unit_details`
  - `pricing`
  - `classification`
  - `inventory`
  - `product_tags`
  - `product_categories`

---

### How the Schema Works

This schema is designed to:
1. **Standardize Product Data**: Ensures a consistent structure for handling product information from multiple sources or vendors.
2. **Improve Searchability**:
   - Fields like `product_tags`, `keywords`, and `long_product_desc` enhance NLP-based search and filtering.
   - `product_categories` enable navigation through a hierarchical system.
3. **Flexibility for Varied Products**:
   - Handles bulk, individual, and variable unit products using `unit_details`.
   - Supports both base and bulk pricing.
4. **Traceability and Metadata**:
   - Timestamps (`created_at`, `last_updated`) enable tracking changes to product information.
   - Vendor-specific fields allow multi-vendor support.

---


## Mercanto Catalog JSON Schema

```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "product_id": {
      "type": "string",
      "description": "Unique identifier for the product."
    },
    "sku": {
      "type": "string",
      "description": "SKU identifier for the product."
    },
    "vendor": {
      "type": "object",
      "properties": {
        "vendor_id": {
          "type": "string",
          "description": "Unique identifier for the vendor."
        },
        "vendor_product_id": {
          "type": "string",
          "description": "Vendor's unique product ID."
        },
        "vendor_name": {
          "type": "string",
          "description": "Name of the vendor."
        }
      },
      "required": ["vendor_id"]
    },
    "product_name": {
      "type": "string",
      "description": "Official name of the product."
    },
    "short_name": {
      "type": "string",
      "description": "Short or alternative name of the product."
    },
    "brand": {
      "type": "string",
      "description": "Brand of the product."
    },
    "description": {
      "type": "string",
      "description": "Detailed description of the product."
    },
    "long_product_desc": {
      "type": "string",
      "description": "Long-form product description with richer details, suitable for marketing purposes."
    },
    "image_url": {
      "type": "string",
      "description": "URL to the product's image."
    },
    "unit_details": {
      "type": "object",
      "properties": {
        "unit_type": {
          "type": "string",
          "enum": ["granel", "pieza", "pieza_variable"],
          "description": "Type of unit for the product."
        },
        "unit_size": {
          "type": "string",
          "description": "Size or weight of the unit (e.g., 1kg, 500ml)."
        },
        "unit_presentation": {
          "type": "string",
          "description": "Presentation format for units (e.g., Caja, Paquete)."
        }
      },
      "required": ["unit_type"]
    },
    "pricing": {
      "type": "object",
      "properties": {
        "base_price": {
          "type": "number",
          "description": "Base price of the product including taxes."
        },
        "bulk_quantity": {
          "type": "number",
          "description": "Quantity required for bulk pricing."
        },
        "bulk_price": {
          "type": "number",
          "description": "Price for bulk quantity including taxes."
        }
      }
    },
    "taxes": {
      "type": "object",
      "properties": {
        "IVA": {
          "type": "boolean",
          "description": "Indicates if IVA applies."
        },
        "IEPS": {
          "type": "boolean",
          "description": "Indicates if IEPS applies."
        },
        "IEPS_rate": {
          "type": "number",
          "description": "Applicable IEPS rate, if IEPS applies."
        }
      }
    },
    "classification": {
      "type": "object",
      "properties": {
        "category": {
          "type": "string",
          "description": "Main category of the product."
        },
        "subcategories": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Subcategories or tags for the product."
        }
      }
    },
    "product_tags": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Non-hierarchical labels for the product (e.g., 'eco-friendly', 'organic')."
    },
    "product_categories": {
      "type": "array",
      "items": {
        "type": "string"
      },
      "description": "Hierarchical, mutually exclusive labels representing product categories (e.g., ['Food', 'Beverages', 'Juices'])."
    },
    "inventory": {
      "type": "object",
      "properties": {
        "available": {
          "type": "boolean",
          "description": "Indicates if the product is available."
        },
        "shopify_ids": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Associated Shopify Collection IDs."
        }
      }
    },
    "metadata": {
      "type": "object",
      "properties": {
        "keywords": {
          "type": "array",
          "items": {
            "type": "string"
          },
          "description": "Keywords for improving searchability."
        },
        "language": {
          "type": "string",
          "description": "Language of the product description."
        },
        "created_at": {
          "type": "string",
          "format": "date-time",
          "description": "Timestamp of when the product entry was created."
        },
        "last_updated": {
          "type": "string",
          "format": "date-time",
          "description": "Timestamp of the last update to the product entry."
        }
      }
    }
  },
  "required": [
    "product_id",
    "product_name",
    "unit_details",
    "pricing",
    "classification",
    "inventory",
    "product_tags",
    "product_categories"
  ]
}
```

---









