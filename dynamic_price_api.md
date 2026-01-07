# Roblox Price & Happy Hour API

This API manages developer product pricing, bulk updates, and "Happy Hour" event state for Roblox experiences.

## Endpoints

### 1. Set Single Price
**POST** `/prices/set`

Updates the price of a single developer product.

**Body (JSON):**
```json
{
  "universe_id": 12345678,
  "name": "100 Coins",
  "price": 50
}
```

### 2. Get Product Info
**POST** `/products/{name}`

Compares a product's price between a source and target universe.

**Body (JSON):**
```json
{
  "source_universe_id": 11111111,
  "target_universe_id": 22222222
}
```

### 3. Get Catalog Comparison
**POST** `/catalog`

Compares all product prices between a source and target universe.

**Body (JSON):**
```json
{
  "source_universe_id": 11111111,
  "target_universe_id": 22222222
}
```

### 4. Restore Prices
**POST** `/prices/restore`

Restores prices in the target universe to match the source universe (asynchronous).

**Body (JSON):**
```json
{
  "target_universe_id": 22222222
}
```

### 5. Set All Prices (Fixed)
**POST** `/prices/set-all`

Sets all products in the target universe to a fixed price (asynchronous).

**Body (JSON):**
```json
{
  "target_universe_id": 22222222,
  "price": 10
}
```

### 6. Set All Prices (Percentage)
**POST** `/prices/set-all-percentage`

Discounts all products by a percentage based on source universe prices (asynchronous).

**Body (JSON):**
```json
{
  "target_universe_id": 22222222,
  "percentage": 50.0  // 50% off
}
```

### 7. Start Happy Hour
**POST** `/happyhour/start`

Enables Happy Hour state (MemoryStore + MessagingService) and optionally updates prices.

**Body (JSON):**
```json
{
  "universe_id": 22222222,
  "ExpireIn": 3600,           // Optional: Duration in seconds
  "Message": "99% OFF SALE!", // Optional
  "MessageColor": "rainbow",  // Optional
  "Percentage": 99.0,         // Optional: Triggers set-all-percentage
  "Price": 1.0                // Optional: Triggers set-all (if percentage not set)
}
```

### 8. End Happy Hour
**POST** `/happyhour/end`

Disables Happy Hour state and restores prices from the source universe.

**Body (JSON):**
```json
{
  "universe_id": 22222222
}
```

## Setup

1.  Set environment variables:
    *   `ROBLOSECURITY`: Cookie for authentication (required for price updates).
    *   `OPEN_CLOUD_API_KEY`: API Key for MemoryStore/MessagingService.
    *   `SOURCE_UNIVERSE_ID`: Default source universe ID for price reference.
2.  Run server: `uvicorn SetPriceApi:app --reload`
