---
ai_level: low
---

# Aliyun CDT Tracker & ECS Control (Cloudflare Worker)

This project runs Aliyun ECS control logic on Cloudflare Workers through Cron Triggers.

It is a serverless replacement for the original `aly_ecs.py` script.

## Prerequisites

- [Node.js](https://nodejs.org/) installed
- Cloudflare Account.

## Setup

1. **Install Dependencies**

   ```bash
   npm install
   ```

2. **Configure Secrets**

   For security, set the following secrets in Cloudflare. Do not commit them to the repository.

   ```bash
   npx wrangler secret put ACCESS_KEY_ID
   # Enter your Aliyun Access Key ID

   npx wrangler secret put ACCESS_KEY_SECRET
   # Enter your Aliyun Access Key Secret

   npx wrangler secret put REGION_ID
   # Enter your region ID (for example: cn-hongkong)

   npx wrangler secret put ECS_INSTANCE_ID
   # Enter your ECS Instance ID

   npx wrangler secret put TRAFFIC_THRESHOLD_GB
   # Enter the threshold (for example: 180). The default is 180 if not set.
   ```

3. **Deploy**

   ```bash
   npx wrangler deploy
   ```

## Configuration

- **Schedule**: By default, the worker runs every 30 minutes. You can change this in `wrangler.toml` under `[triggers]`.
  ```toml
  [triggers]
  crons = ["*/30 * * * *"]
  ```

## Development

- **Local Test (Trigger via HTTP)**

   During development, you can trigger the logic manually by visiting the worker URL, for example while using `wrangler dev`.

  ```bash
  npx wrangler dev
  ```
