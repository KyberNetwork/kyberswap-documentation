---
description: Complete HTTP API reference for all ZaaS endpoints.
---

# API Reference

## API Reference

**Base URL:** `https://zap-api.kyberswap.com/{chain}`

All requests must include the `X-Client-ID` header. Without a whitelisted ID, the default rate limit is **10 requests per 10 seconds**. Contact [bd@kyber.network](mailto:bd@kyber.network) to request a higher quota.

### Endpoints

| Method | Path                          | Description                                                     |
| ------ | ----------------------------- | --------------------------------------------------------------- |
| `GET`  | `/api/v1/in/route`            | Get the best Zap-In route for a given input and target position |
| `POST` | `/api/v1/in/route/build`      | Build on-chain calldata for a confirmed Zap-In route            |
| `GET`  | `/api/v1/migrate/route`       | Get the best Zap-Migrate route between two pools                |
| `POST` | `/api/v1/migrate/route/build` | Build on-chain calldata for a confirmed Zap-Migrate route       |
| `GET`  | `/api/v1/out/route`           | Get the best Zap-Out route for exiting a position               |
| `POST` | `/api/v1/out/route/build`     | Build on-chain calldata for a confirmed Zap-Out route           |
