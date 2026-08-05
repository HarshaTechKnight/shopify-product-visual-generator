# E-commerce Product Visual Generator

<img width="1366" height="599" alt="shopify-screenshot" src="https://github.com/user-attachments/assets/372f77f0-246d-4aeb-a598-9db8134899e8" />


An automated n8n workflow that generates professional studio-quality product photos and transparent PNG catalog cutouts whenever new products are created in **Shopify**.

By combining **Anthropic's Claude** AI model with **deAPI's** image generation and background removal capabilities, this workflow automates the product imagery pipeline from creation to storefront update.

---

## 🌟 Key Features

* **Automatic Triggering:** Listens to `products/create` webhooks directly from Shopify[cite: 3].
* **AI Prompt Optimization:** Uses an Anthropic AI Agent along with deAPI's **Image Prompt Booster** tool to generate optimized prompts for e-commerce photography[cite: 3].
* **Dual-Image Generation:**
  1. **Styled Hero Image:** A high-quality studio/lifestyle photo based on product attributes[cite: 3].
  2. **Transparent PNG:** Background-removed version ideal for catalog views and promotional graphics[cite: 3].
* **Automated Shopify Ingestion:** Automatically uploads both generated images to the target product in Shopify (Position 1 for hero, Position 2 for cutout)[cite: 3].
* **Structured JSON Output:** Utilizes a Structured Output Parser to guarantee valid prompt formatting for image generation[cite: 3].

---

## 📐 Workflow Architecture & Steps

### 1. Shopify Product Trigger
* **Node:** `Shopify Trigger`
* Listens for the `products/create` webhook event when a new item is added to the catalog[cite: 3].

### 2. Extract Product Data
* **Node:** `Edit Fields`
* Filters key context attributes (Title, Description, Category, Tags) to build context for the AI prompt builder[cite: 3].

### 3. AI-Powered Prompt Generation
* **Nodes:** `AI Agent`, `Anthropic Chat Model` (Claude Sonnet 4.5), `Image prompt booster in deAPI`, `Structured Output Parser`
* The AI Agent processes the product metadata, calls deAPI's Prompt Booster tool, and outputs a formatted JSON object containing `boosted_prompt`[cite: 3].

### 4. Generate Product Image
* **Node:** `deAPI Generate Image`
* Takes the boosted prompt and generates a studio-quality product image[cite: 3].

### 5. Remove Background
* **Node:** `deAPI Remove Background`
* Processes the generated hero image and outputs a clean, transparent PNG cutout[cite: 3].

### 6. Update Product Images
* **Node:** `Shopify Update Product`
* Uploads both images back to the newly created Shopify product[cite: 3]:
  * **Position 1 (Main):** Styled Hero Image[cite: 3]
  * **Position 2 (Alt):** Transparent PNG[cite: 3]

---

## 🛠️ Prerequisites

To run this workflow, ensure you have credentials/accounts configured for:

1. **n8n Instance** (v1.x or higher with LangChain support)
2. **Shopify Store Account** with custom app permissions:
   * `read_products`[cite: 3]
   * `write_products`[cite: 3]
   * `write_files`[cite: 3]
   * Webhook URL configured with **HTTPS**[cite: 3]
3. **deAPI Account** for image generation and background removal[cite: 3]
4. **Anthropic API Key** (for Claude language model processing)[cite: 3]

---

## ⚙️ Setup & Configuration

1. **Shopify Integration:**
   * Set up the **Shopify Trigger** node with your shop credentials and subscribe to the `products/create` topic[cite: 3].
2. **deAPI Setup:**
   * Add your deAPI credentials in n8n for both image generation, background removal, and the deAPI Tool node[cite: 3].
3. **AI Agent Setup:**
   * Configure the **Anthropic Chat Model** node with your Anthropic API Key[cite: 3].
4. **Publish Workflow:**
   * Activate the workflow in n8n. Whenever a product is published on Shopify, image generation will execute automatically![cite: 3]

---

## 📝 License

This workflow is available under the [MIT License](LICENSE).
