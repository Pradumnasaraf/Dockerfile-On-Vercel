## Dockerfile on Vercel

A tiny Go web app packaged as a container, ready to deploy on [Vercel's Dockerfile support](https://vercel.com/blog/dockerfile-on-vercel). It responds over HTTP with a simple greeting and a health check.

Add a `Dockerfile.vercel`, make sure the app listens on `$PORT` (defaults to `80`) and speaks HTTP, then run `vercel deploy`. Vercel builds the image and runs it on Fluid compute.

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new/clone?repository-url=https://github.com/Pradumnasaraf/Dockerfile-On-Vercel)

### What's here

| File                | Purpose                                                |
| ------------------- | ------------------------------------------------------ |
| `main.go`           | HTTP server, listens on `$PORT` (falls back to 8080)   |
| `Dockerfile.vercel` | Multi-stage build to a distroless runtime image        |
| `go.mod`            | Module definition (stdlib only, no dependencies)       |

### Endpoints

- `GET /`: plain text greeting
- `GET /health`: returns `ok`

### Run locally

With Go:

```bash
go run .
```

With Docker:

```bash
docker build -f Dockerfile.vercel -t dockerfile-on-vercel .
docker run --rm -p 8080:80 -e PORT=80 dockerfile-on-vercel
```

Then open http://localhost:8080.

### Deploy to Vercel

Use the button above, or run `vercel deploy`. Vercel detects `Dockerfile.vercel`, builds the image, and runs it on Fluid compute, with autoscaling, per-request pricing, and a preview URL on every push. Containers are stateless, so use a database or cache for anything that must persist.

### License

Licensed under the [Apache 2.0](LICENSE) License.
