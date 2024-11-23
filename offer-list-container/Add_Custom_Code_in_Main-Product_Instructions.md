# Instructions

## Adding Liquid and HTML Code

### Add the custom code in the `main-product.liquid` file
Place the custom code between the following lines:

```liquid
{%- for block in section.blocks -%}
...
{%- endfor -%}
```
## Code Example:
```liquid
<product-info
  id="ProductInfo-{{ section.id }}"
  data-section="{{ section.id }}"
  data-url="{{ product.url }}"
  class="product__info-container{% if section.settings.enable_sticky_info %} product__column-sticky{% endif %}"
>
  {%- assign product_form_id = 'product-form-' | append: section.id -%}

  {%- for block in section.blocks -%}
    {%- case block.type -%}
      {%- when '@app' -%}
        {% render block %}

        ********************************
        *** Add the custom code here ***
        ********************************

   {%- endfor -%}
```
## Custom Code:
```liquid
  <!-- offer list container custom code start -->
  {%- when 'offer_container' -%}
    <div>
      {%- for block in section.blocks -%}
        {%- if block.type == 'offer_container' -%}
          {%- render 'offer-list-container',
            offer_products: block.settings.offer_products,
            offer_prices: block.settings.offer_prices,
            include_free_shipping: block.settings.include_free_shipping,
            free_shipping_image: block.settings.free_shipping_image,
            normal_shipping_value: block.settings.normal_shipping_value
          -%}
        {%- endif -%}
      {%- endfor -%}
    </div>
  <!-- offer list container custom code end -->
```
## Adding Schema
### Add the custom Schema code in the main-product.liquid file
### Insert the custom Schema code within the blocks: [...] section between {%- schema -%} and {%- endschema -%}.

## Code Example:
```liquid
{% schema %}
{
  "name": "t:sections.main-product.name",
  "tag": "section",
  "class": "section",
  "blocks": [
    {
      "type": "@app"
    },
    *** Paste the custom Schema code here ***
    {
      ... other Schema structures ...
    },
    {
      ... other Schema structures ...
    }
  ]
}
{% endschema %}
```

## Custom Schema Code:
```JSON
{
  "type": "offer_container",
  "name": "Offer List Container",
  "settings": [
    {
      "type": "product_list",
      "id": "offer_products",
      "label": "Offer Products",
      "limit": 10,
      "info": "Select products to include in the offer. These products will display their original and offered prices."
    },
    {
      "type": "text",
      "id": "offer_prices",
      "label": "Offered Prices (Comma-Separated)",
      "info": "Enter the offered prices in cent value for each product in the same order as selected products. Use '0' for Free. Separate values with commas."
    },
    {
      "type": "checkbox",
      "id": "include_free_shipping",
      "label": "Include Free Shipping",
      "default": false,
      "info": "Check this option to include free shipping as part of the offer."
    },
    {
      "type": "image_picker",
      "id": "free_shipping_image",
      "label": "Upload Free Shipping Image",
      "info": "Upload an image for Free Shipping"
    },
    {
      "type": "text",
      "id": "normal_shipping_value",
      "label": "Normal Shipping Value",
      "default": "0",
      "info": "Enter the value of Normal Shipping in cent value"
    }
  ]
}
```
