# Ionic Rewards api

## Ionic Rewards Indexer API Documentation

#### API Base URL

Use the following base URL for API requests:

```
https://api.ionic.ninja
```

### API Endpoints

#### 1. Get User Rewards

#### API Request to Retrieve User Rewards

**Endpoint**: `GET https://api.ionic.ninja/api/rewards/{chain}/{user}`

**Description**: This endpoint retrieves the total rewards and the ION token address for a specific user on a specified blockchain network.

**Parameters**

| Parameter | Type   | Required | Description                                    |
| --------- | ------ | -------- | ---------------------------------------------- |
| `chain`   | string | Yes      | Name of the network (either 'mode' or 'base'). |
| `user`    | string | Yes      | Ethereum wallet address .                      |

**Examples**

### Network Requests

#### Mode Network Request

To make a network request to the Mode API, use the following command:

```bash
curl https://api.ionic.ninja/api/rewards/mode/0x742d35Cc66xxxxxxxxxxxxxxxxxxxxxxx
```

#### Base Network Request

To make a network request to the Base API, use the following command:

```bash
curl https://api.ionic.ninja/api/rewards/base/0x742d35Cc6634Cxxxxxxxxxxxxxxxxxxxx
```



**HTTP Status Code:** 200 OK

**Response:**

```json
{
  "chain": "mode",
  "user": "0x742d35cc6634c0532925a3b844bc454e4438f44e",
  "totalRewards": "1000000000000000000",
  "ionTokenAddress": "0x18470019bF0E94611f15852F7e93cf5D65BC34CA"
}
```

### Error Responses

#### 400 Bad Request

```json
{
  "error": "Invalid chain. Supported chains are: mode, base."
}
```

#### 500 Internal Server Error

```json
{
  "error": "Failed to fetch user rewards data."
}
```

Ensure to verify the chain type and retry the request. For persistent issues, please contact support.

### Network-Specific Details

#### Mode Network

* Chain ID: 34443
* ION Token Address: 0x18470019bF0E94611f15852F7e93cf5D65BC34CA

#### Base Network

* Chain ID: 8453
* ION Token Address: 0x3eE5e23eEE121094f1cFc0Ccc79d6C809Ebd22e5

| Field           | Type   | Description                                                             |
| --------------- | ------ | ----------------------------------------------------------------------- |
| chain           | string | The blockchain network, either "mode" or "base."                        |
| user            | string | The user's Ethereum address (in lowercase).                             |
| totalRewards    | string | Total rewards in Wei (represented as a string to manage large numbers). |
| ionTokenAddress | string | The ION token contract address for the specified chain                  |

### Notes

* All addresses are returned in lowercase format
* No authentication is required for these endpoints
