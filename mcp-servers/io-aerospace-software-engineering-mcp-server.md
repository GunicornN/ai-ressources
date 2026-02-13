---
title: "IO Aerospace MCP Server"
url: "https://github.com/IO-Aerospace-software-engineering/mcp-server"
description: "#️⃣ ☁️/🏠 🐧 - IO Aerospace MCP Server: a .NET-based MCP server for aerospace & astrodynamics — ephemeris, orbital conversions, DSS tools, time conversions, and unit/math utilities. Supports STDIO and SSE transports; Docker and native .NET deployment documented."
sourceRepo: "IO-Aerospace-software-engineering/mcp-server"
tags: ["MCP", "IA", "TypeScript"]
date: 2026-02-13
language: "en"
stars: 14
forks: 2
---

# IO Aerospace MCP Server

## Use it now
> Hosted in production (no setup needed): https://mcp.io-aerospace.org/
>
> **Transport Protocols:**
> - **Streamable-HTTP** (recommended): https://mcp.io-aerospace.org/ - Modern MCP transport protocol
> - **SSE** (legacy): https://mcp.io-aerospace.org/sse - For backward compatibility with older MCP clients only
>
> Note: Use the base URL with modern MCP clients - they will automatically use the streamable-HTTP transport. Only use the `/sse` endpoint if you have an older client that specifically requires SSE protocol.

A Model Context Protocol (MCP) server for aerospace and astrodynamics calculations, providing tools for celestial body ephemeris, orbital mechanics, and space mission analysis.

## Overview

This MCP server provides two transport options:
- **STDIO Transport**: Standard input/output communication (recommended for local MCP clients)
- **HTTP Transport**: Supports both modern streamable-HTTP and legacy SSE protocols for web-based integrations
  - **Streamable-HTTP** (default, recommended): Modern MCP protocol at the base URL
  - **SSE** (legacy): Available at `/sse` endpoint for backward compatibility only

The server includes comprehensive tools for:
- Celestial body ephemeris and state vector calculations
- Orbital mechanics and geometry computations
- Deep Space Network (DSN) ground station operations
- Solar system object properties and characteristics
- Mathematical conversions for aerospace calculations
- Time system conversions and utilities

## Astrodynamics Framework

This server is powered by the IO Aerospace Astrodynamics framework, which provides the core algorithms for ephemerides, orbital mechanics, geometry, and time systems.

- Repository: https://github.com/IO-Aerospace-software-engineering/Astrodynamics

## Use the hosted server (recommended)

You can start integrating immediately against the production instance:
- **Base URL (streamable-HTTP)**: https://mcp.io-aerospace.org/ - Use this with modern MCP clients
- **SSE endpoint (legacy)**: https://mcp.io-aerospace.org/sse - Only for older clients requiring SSE protocol

**Important**: Modern MCP clients (2024+) should use the base URL with streamable-HTTP transport. The SSE endpoint is maintained only for backward compatibility with older implementations.

Example (legacy SSE - browser/Node):
```javascript
// Only use this if you have an old client that requires SSE
const eventSource = new EventSource('https://mcp.io-aerospace.org/sse');

eventSource.onmessage = (event) => {
  console.log('message', event.data);
};

eventSource.onerror = (err) => {
  console.error('sse error', err);
};
```

Self-hosting is optional; see below for Docker and .NET instructions.

## Project Structure

```
mcp-server/
├── AI/                           # AI tools and models
│   ├── Tools/                    # Core calculation tools
│   ├── Models/                   # Data models and types
│   └── Converters/              # Type converters
├── Data/                         # Data providers and solar system kernels
│   ├── SolarSystem/             # SPICE kernel files
│   └── SolarSystemObjects/      # Celestial body definitions
├── Server.Http/                 # HTTP transport server (streamable-HTTP + legacy SSE)
├── Server.Stdio/                # STDIO transport server
├── docker-compose.yml           # Development Docker configuration
├── docker-compose.prod.example.yml  # Production template
└── deploy-production.sh         # Production deployment script
```

## Prerequisites

- .NET 9.0 SDK or runtime
- Docker (for containerized deployment)
- Solar system kernels data (SPICE kernels)

## Available Tools

### CelestialBodyTools
- **GetEphemerisAsStateVectors**: Calculate state vectors (position and velocity) of celestial bodies
- **GetCelestialBodyProperties**: Retrieve geophysical properties of planets and moons

### OrbitalParametersTools
- **ConvertStateVectorToKeplerianElements**: Convert state vectors to Keplerian orbital elements
- **ConvertStateVectorToEquinoctialElements**: Convert state vectors to equinoctial elements
- **ConvertStateVectorToEquatorialCoordinates**: Convert state vectors to equatorial coordinates
- **ConvertKeplerianElementsToStateVector**: Convert Keplerian elements back to state vectors
- **ConvertEquinoctialElementsToStateVector**: Convert equinoctial elements back to state vectors
- **ConvertStateVectorToTheGivenFrame**: Transform state vectors between reference frames

### GeometryFinderTools
- **FindCoordinateConstraint**: Find time windows when coordinate constraints are met
- **FindDistanceConstraint**: Find time windows when distance constraints are satisfied
- **FindOccultingConstraint**: Find occultation and eclipse events

### SiteTools
- **GetDeepSpaceStationPlanetodeticCoordinates**: Get latitude, longitude, and altitude of DSS stations
- **GetDeepSpaceStationStateVector**: Calculate state vectors for ground stations
- **GetHorizontalCoordinates**: Get azimuth and elevation from ground stations
- **GetDSSFrame**: Retrieve reference frame information for DSS stations

### TimeTools
- **ConvertDateTime**: Convert between different time systems (UTC, TDB, TAI, TDT, GPS)
- **CurrentDateTime**: Get current UTC date and time

### MathTools
- **DegreesToRadians** / **RadiansToDegrees**: Angular unit conversions
- **ConvertDegreesToHours** / **ConvertHoursToDegrees**: Time-angle conversions
- **DegreesToArcseconds** / **ArcsecondsToDegrees**: Angular precision conversions
- **RadiansToArcseconds** / **ArcsecondsToRadians**: Angular unit conversions
- **MetersToMiles** / **MilesToMeters**: Distance unit conversions
- **MetersToFeet** / **FeetToMeters**: Distance unit conversions
- **MetersToKilometers** / **KilometersToMeters**: Metric distance conversions
- **MetersToAstronomicalUnits** / **AstronomicalUnitsToMeters**: Astronomical distance conversions
- **MetersToParsec** / **ParsecToMeters**: Stellar distance conversions
- **MetersToLightYears** / **LightYearsToMeters**: Cosmic distance conversions

## Quick Start (self-hosting)

### Docker Deployment

#### Development
```bash
git clone https://github.com/IO-Aerospace-software-engineering/mcp-server
cd mcp-server
docker-compose up
```

The HTTP server will be available at `http://localhost:8080`.

#### Production
1. Copy `docker-compose.prod.example.yml` to `docker-compose.prod.yml`
2. Update the domain names in the production file
3. Ensure kernel data exists at `./data/solarsystem/`
4. Deploy using the automated script:

```bash
./deploy-production.sh
```

### Native .NET Deployment

#### 1. Clone and Build
```bash
git clone https://github.com/IO-Aerospace-software-engineering/mcp-server
cd mcp-server
dotnet build
```

#### 2. Solar System Data Setup

The server requires SPICE kernels for solar system calculations.

- STDIO server configuration (no appsettings):
  - Provide the kernels path via CLI or environment variable
  - Priority: CLI flag > IO_DATA_DIR environment variable
  - CLI flags: `-k <path>`, `--kernels <path>`, or `--kernels-path <path>`

Examples:
```bash
# Using CLI flag
./Server.Stdio -k /path/to/your/spice/kernels

# Using environment variable (Linux/macOS)
export IO_DATA_DIR="/path/to/your/spice/kernels"
./Server.Stdio

# Windows (PowerShell)
$env:IO_DATA_DIR="C:\path\to\your\spice\kernels"
./Server.Stdio.exe
```

- HTTP server configuration: may use appsettings.json as before.

**Required Kernel Files:**
```
kernels/
├── de440s.bsp              # Planetary ephemeris
├── latest_leapseconds.tls  # Leap seconds
├── pck00011.tpc           # Planetary constants
├── earth_latest_high_prec.bpc  # Earth orientation
└── ...                    # Additional kernel files
```

#### 3. Choose Transport Method

##### STDIO Transport (For MCP Clients)
- Release assets are native executables per OS/RID (no ZIP). Filenames:
  - mcp-server-stdio-<tag>-linux-x64
  - mcp-server-stdio-<tag>-win-x64.exe
  - mcp-server-stdio-<tag>-osx-arm64
- On macOS, a sidecar native library may be provided (e.g., libIO.Astrodynamics.so). Place it in the same directory as the executable.

```bash
# After publishing or downloading a release asset for your OS
./Server.Stdio -k /path/to/kernels
```

###### HTTP Transport (For Web/HTTP)
```bash
cd Server.Http
dotnet run
# Server available at http://localhost:8080
``

## Docker Configuration

### Development Environment
- **File**: `docker-compose.yml`
- **Ports**: 8080 (HTTP), 8081 (HTTPS)
- **Data**: Mounted from `./Data/SolarSystem`
- **Usage**: `docker-compose up`

### Production Environment
- **File**: `docker-compose.prod.yml` (create from example)
- **Features**: Traefik reverse proxy, optimized images
- **Data**: Host-mounted from `./data/solarsystem`
- **Deployment**: Automated via `deploy-production.sh`

## MCP Client Integration

Note: Many MCP clients use JSON-based configuration files, but schemas differ per client. The JSON examples below use Claude Desktop’s schema; adapt keys to your client’s format.

### Claude Desktop Configuration (STDIO)
Add to your Claude Desktop configuration:

```json
{
  "mcpServers": {
    "astrodynamics": {
      "command": "/path/to/Server.Stdio",
      "args": ["-k", "/path/to/kernels"]
    }
  }
}
```

Alternatively, set an environment variable if your client supports it:

```json
{
  "mcpServers": {
    "astrodynamics": {
      "command": "/path/to/Server.Stdio",
      "args": [],
      "env": {
        "IO_DATA_DIR": "/path/to/kernels"
      }
    }
  }
}
```

### Claude Desktop Configuration (HTTP transport to hosted server)
Use your production server over HTTP by specifying the base URL only. Modern MCP clients will use streamable-HTTP:

```json
{
  "mcpServers": {
    "astrodynamics": {
      "transport": {
        "type": "http",
        "url": "https://mcp.io-aerospace.org"
      }
    }
  }
}
```

- The base URL uses the modern **streamable-HTTP** transport protocol
- Do NOT append `/sse` - that's only for legacy SSE clients
- This schema is for Claude Desktop; other clients may use different keys

### Other MCP clients
- Provide the base URL: https://mcp.io-aerospace.org
- Add headers (e.g., Authorization) only if your deployment requires it
- Don’t append `/sse` unless your client documentation requires it; most discover the SSE path
- Refer to your client’s documentation for the exact JSON schema or settings UI

### Node.js MCP client (streamable-HTTP)
Using the MCP SDK to connect to the hosted server with modern streamable-HTTP transport:

```ts
import { Client } from "@modelcontextprotocol/sdk/client/index.js";
import { HttpClientTransport } from "@modelcontextprotocol/sdk/client/transport/http.js";

// Modern streamable-HTTP transport (recommended)
const transport = new HttpClientTransport(new URL("https://mcp.io-aerospace.org"));
const client = new Client(
  { name: "example-client", version: "1.0.0" },
  { capabilities: { tools: {}, prompts: {}, resources: {} } },
  transport
);

await client.connect();
const tools = await client.listTools();
console.log("Tools:", tools);

// Example: call a tool
// const result = await client.callTool({ name: "GetEphemerisAsStateVectors", arguments: { /* ... */ } });
// console.log(result);
```

## Sponsor

If this project helps your work, please consider sponsoring ongoing development, hosting, and data updates.

- Sponsor page: https://github.com/sponsors/IO-Aerospace-software-engineering
- Businesses: open an issue to discuss invoices or custom arrangements

Your support helps keep the hosted server online and the SPICE data current.

## Troubleshooting

### Common Issues

1. "Kernels directory does not exist": Verify the path passed with `-k` (or `IO_DATA_DIR`) exists and contains SPICE files
2. "Failed to load kernel": Ensure all required kernel files are present and accessible
3. Connection errors: Check firewall settings and port availability

### Log Monitoring
```bash
# Development
docker-compose logs -f

# Production
docker logs -f container-name
```

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and questions:
- Create an issue on GitHub
- Check the troubleshooting section above
- Review the deployment guide in [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md)

Sylvain

> New: A step-by-step How To guide is available:
> - Markdown: [docs/HowTo.md](docs/HowTo.md)
> - HTML (full): [docs/howto.html](docs/howto.html)
> - HTML (compact): [docs/howto-mini.html](docs/howto-mini.html)
