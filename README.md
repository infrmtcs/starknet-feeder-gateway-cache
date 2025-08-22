# Starknet Feeder Gateway Cache

A caching proxy for Starknet feeder gateways and gateways, built with Nginx. This service provides cached access to Starknet API endpoints across multiple networks.

## Quick Start

### Prerequisites

- Docker and Docker Compose installed
- Optional: Juno Gateway API key for enhanced rate limits

### Running the Service

1. (Optional) Configure your Juno Gateway API key in the `.env` file:
   ```bash
   JUNO_GW_API_KEY="your-api-key-here"
   ```

2. Start the service:
   ```bash
   docker compose up -d
   ```

The service will be available at `http://localhost:8080`

### Clearing the Cache

The cache is stored in the `./cache` directory and persists between container restarts. To clear the cache:

   ```bash
   rm -rf ./cache
   ```

## API Usage

### Endpoint Structure

All endpoints follow the pattern:
```
http://localhost:8080/{network}/{service}/{endpoint}
```

Where:
- `{network}` can be: `mainnet`, `sepolia`, or `integration-sepolia`
- `{service}` can be: `feeder_gateway` or `gateway`
- `{endpoint}` is the specific API endpoint

Requests with query parameter `block_number=latest` or `block_number=pending` won't be cached.


### Example Usage

```bash
curl "http://localhost:8080/mainnet/feeder_gateway/get_state_update?blockNumber=1&includeBlock=true"
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
