# pulumi-datamammoth

Pulumi provider for DataMammoth -- manage VPS servers, products, and infrastructure as code.

## Status

This provider will be **bridged from the Terraform provider** using
[pulumi-terraform-bridge](https://github.com/pulumi/pulumi-terraform-bridge).

The upstream Terraform provider lives at
[datamammoth/terraform-provider-datamammoth](https://github.com/datamammoth/terraform-provider-datamammoth).

## Planned Resources

| Resource | Description |
|---|---|
| `datamammoth:Server` | Provision and manage VPS instances |
| `datamammoth:Firewall` | Server firewall rules |
| `datamammoth:Snapshot` | Server snapshots |
| `datamammoth:Webhook` | Webhook endpoints |

## Planned Data Sources

| Data Source | Description |
|---|---|
| `datamammoth:getProducts` | List available hosting products |
| `datamammoth:getZones` | List hosting zones / regions |
| `datamammoth:getImages` | List OS images for a zone |

## Usage (Preview)

```typescript
import * as datamammoth from "@pulumi/datamammoth";

const server = new datamammoth.Server("web-1", {
    productId: "prod_vps_4core",
    region: "EU",
    imageId: "ubuntu-24.04",
    hostname: "web-1.example.com",
});

export const serverIp = server.ipAddress;
```

```python
import pulumi_datamammoth as datamammoth

server = datamammoth.Server("web-1",
    product_id="prod_vps_4core",
    region="EU",
    image_id="ubuntu-24.04",
    hostname="web-1.example.com",
)

pulumi.export("server_ip", server.ip_address)
```

## Building from Source

```bash
# 1. Clone the Terraform provider
git clone https://github.com/datamammoth/terraform-provider-datamammoth

# 2. Generate the bridge
cd pulumi-datamammoth
make tfgen        # generates Pulumi schema from Terraform schema
make provider     # builds pulumi-resource-datamammoth binary

# 3. Generate SDKs
make build_sdks   # generates Node.js, Python, Go, .NET SDKs
```

## Configuration

| Key | Environment Variable | Description |
|---|---|---|
| `datamammoth:apiKey` | `DATAMAMMOTH_API_KEY` | API key (`dm_live_...`) |
| `datamammoth:baseUrl` | `DATAMAMMOTH_BASE_URL` | Override API URL (self-hosted) |

## License

MIT
