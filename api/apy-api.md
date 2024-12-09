# API

### APY API

**Endpoint: `GET /asset-total-apy`**

**Description**: Retrieve data from the `asset-total-apy` table.

* **Base URL**: `https://uoagtjstsdrjypxlkuzr.supabase.co/rest/v1`

**Reading Rows:**

1.  **Read All Rows**

    Retrieve all rows:

    ```bash
    curl 'https://uoagtjstsdrjypxlkuzr.supabase.co/rest/v1/asset-total-apy?select=*' \
    -H "apikey: SUPABASE_CLIENT_ANON_KEY" \
    -H "Authorization: Bearer SUPABASE_CLIENT_ANON_KEY" 
    ```

#### Example Response

If the request is successful, you will receive data in a format similar to the following:

```json
[
  {
    "id": 1,
    "created_at": "2024-06-18T11:00:05.509771+00:00",
    "chain_id": "8453",
    "underlying_address": "0x940181a94a35a4569e4529a3cdfb74e38fd98631",
    "ctoken_address": "0x014e08f05ac11bb532be62774a4c548368f59779",
    "totalSupplyApy": "5.301877254953391",
    "supplyApy": "5.301877254953391",
    "borrowApy": "12.214642575076851"
  },
]
```

#### Query a Specific Asset

To query for a specific asset, use the following template. You can filter by chain using `?chain_id=eq.10`. Replace `eq.` with the appropriate filter condition as needed:

```bash
curl 'https://uoagtjstsdrjypxlkuzr.supabase.co/rest/v1/asset-total-apy?chain_id=eq.10' \
-H "apikey: SUPABASE_CLIENT_ANON_KEY" \
-H "Authorization: Bearer SUPABASE_CLIENT_ANON_KEY"
```

For example, to retrieve data for chain ID 10, use `?chain_id=eq.10`. This will return results such as:

```json
[
  {
    "id": 108616,
    "created_at": "2024-11-20T11:00:24.541747+00:00",
    "chain_id": "10",
    "underlying_address": "0x68f180fcce6836688e9084f035309e29bf0a2095",
    "ctoken_address": "0x863dccaad60a1105f4b948c67895b4f0411c4497",
    "totalSupplyApy": "0",
    "supplyApy": "0",
    "borrowApy": null
  },
  {
  "id":108610,
  "created_at":"2024-11-20T11:00:24.541747+00:00",
  "chain_id":"10",
  "underlying_address":"0x4200000000000000000000000000000000000006",
  "ctoken_address":"0x53b1d15b24d93330b2fd359c798de7183255e7f2",
  "totalSupplyApy":"7.831698780438984",
  "supplyApy":"0.4228539648305496",
  "borrowApy":"3.1290958796524437"
  }
  ...
]
```

#### Read Specific Columns

Retrieve only certain columns:

```bash
curl 'https://uoagtjstsdrjypxlkuzr.supabase.co/rest/v1/asset-total-apy?select=some_column,other_column' \
-H "apikey: SUPABASE_CLIENT_ANON_KEY" \
-H "Authorization: Bearer SUPABASE_CLIENT_ANON_KEY"
```

#### Available Columns

The following columns are available in the `asset-total-apy` table:

* `created_at`
* `chain_id`
* `underlying_address`
* `ctoken_address`
* `totalSupplyApy`
* `supplyApy`
* `borrowApy`

#### With Pagination

Retrieve data with pagination:

```bash
curl 'https://uoagtjstsdrjypxlkuzr.supabase.co/rest/v1/asset-total-apy?select=*' \
-H "apikey: SUPABASE_CLIENT_ANON_KEY" \
-H "Authorization: Bearer SUPABASE_CLIENT_ANON_KEY" \
-H "Range: 0-9"
```

Check the folder below to find the **SUPABASE\_CLIENT\_ANON\_KEY**

<details>

<summary>KEY</summary>

```
SUPABASE_CLIENT_ANON_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6InVvYWd0anN0c2RyanlweGxrdXpyIiwicm9sZSI6ImFub24iLCJpYXQiOjE3MDc5MDE2MTcsImV4cCI6MjAyMzQ3NzYxN30.CYck7aPTmW5LE4hBh2F4Y89Cn15ArMXyvnP3F521S78
```

</details>

Please note: If the provided key does not work, please contact the Ionic team to request a new key.
