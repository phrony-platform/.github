<p align="center">
  <img
    src="https://raw.githubusercontent.com/phrony-platform/runtime/main/assets/phrony-runtime-logo.png"
    alt="Phrony"
    width="480"
  />
</p>

<h3 align="center">Agents as first-class primitives — declared, deployed, and run.</h3>

<p align="center">
  <a href="https://docs.phrony.com">Documentation</a>
  ·
  <a href="https://docs.phrony.com/quick-start">Quick start</a>
  ·
  <a href="https://docs.phrony.com/agent-spec">Agent spec</a>
  ·
  <a href="https://phrony.com">phrony.com</a>
</p>

---

**Phrony** is an open stack for production agents: a declarative **Agent Spec**, a reference **runtime** that executes manifests, and SDKs and examples for applications and tool workers.

Instead of embedding an agent loop in application code, you **declare** the agent in versioned YAML, **deploy** a named version to the runtime, and **run** it through `phrony` or gRPC — the runtime owns the model loop, tools, policies, limits, human-in-the-loop, and traces.

```text
declare  →  agent.yaml in git (tools, policies, secrets, limits)
deploy   →  phrony deploy namespace/my-agent@1.0.0
run      →  phrony session …  ·  SDK  ·  gRPC RunSession
```

## Repositories

| Repository | What it is |
| --- | --- |
| [runtime](https://github.com/phrony-platform/runtime) | Official open-source **Phrony Agent Spec** runtime (`phrony-runtime` daemon, `phrony` operator CLI, gRPC API) |
| [typescript-sdk](https://github.com/phrony-platform/typescript-sdk) | **`@phrony/sdk`** — TypeScript client for agents, interactive sessions, and tool workers |
| [tool-worker-playground](https://github.com/phrony-platform/tool-worker-playground) | Minimal Go **tool worker** example (Work stream, dispatch, HITL) |

## Get started in five minutes

1. Clone and start the runtime (Postgres + gRPC on `127.0.0.1:7777`):

   ```bash
   git clone https://github.com/phrony-platform/runtime.git
   cd runtime && make dev-up
   ```

2. Install the operator CLI and check the daemon:

   ```bash
   make install-cli
   phrony status
   ```

3. Follow the [quick start](https://docs.phrony.com/quick-start): write a manifest, validate, deploy, and run a session.

For TypeScript applications talking to a local runtime:

```bash
pnpm add @phrony/sdk
```

```typescript
import { Phrony } from "@phrony/sdk";

const phrony = await Phrony.connect();
const result = await phrony.agent("default/my-agent").run({
  input: { question: "hello" },
});
console.log(result.output);
phrony.close();
```

See the [typescript-sdk](https://github.com/phrony-platform/typescript-sdk) README for workers, streaming sessions, and integration tests.

## Learn more

- **[Paradigm](https://docs.phrony.com/paradigm)** — why agents need their own primitive
- **[Agent spec](https://docs.phrony.com/agent-spec)** — manifest format (`phrony.com/v1`)
- **[Runtime](https://docs.phrony.com/runtime)** — install, CLI, tool dispatch, MCP tools, durability, HITL

## Contributing

Issues and pull requests are welcome in each repository. For the runtime, see [CONTRIBUTING](https://github.com/phrony-platform/runtime/blob/main/CONTRIBUTING.md).

## License

Open-source components in this organization are released under **MIT** unless a repository states otherwise.
