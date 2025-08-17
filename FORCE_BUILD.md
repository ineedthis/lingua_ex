# Force Building From Source

When using this library as a dependency, you may encounter issues with hardcoded repository references in the precompiled binaries downloaded from Hex. Here are several ways to force building from source:

## Method 1: Environment Variables

Set one of these environment variables to force building from source:

```bash
# Option 1: Original variable
export LINGUA_BUILD=1

# Option 2: Alternative variable
export LINGUA_FORCE_BUILD=1
```

Then run your mix commands:
```bash
mix deps.get
mix compile
```

## Method 2: Runtime Configuration

Add this to your `config/config.exs`:

```elixir
config :rustler_precompiled, :force_build, lingua: true
```

## Method 3: Mix Environment Variable

Set the environment variable when running mix:

```bash
LINGUA_BUILD=1 mix deps.get
LINGUA_BUILD=1 mix compile
```

## Method 4: Docker/Production

For Docker or production environments, add the environment variable to your Dockerfile:

```dockerfile
ENV LINGUA_BUILD=1
```

Or in your docker-compose.yml:

```yaml
environment:
  - LINGUA_BUILD=1
```

## Method 5: CI/CD

For GitHub Actions or similar CI systems:

```yaml
env:
  LINGUA_BUILD: 1
```

## Troubleshooting

If you're still getting errors about downloading from the original repository, try:

1. Delete your `deps/lingua` directory
2. Set the environment variable
3. Run `mix deps.get` again

```bash
rm -rf deps/lingua
LINGUA_BUILD=1 mix deps.get
LINGUA_BUILD=1 mix compile
```

This forces a complete rebuild from your updated source.
