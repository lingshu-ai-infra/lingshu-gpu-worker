# lingshu-gpu-worker

GPU worker process that executes scheduled operator tasks.

## Components

- **OpRegistry** — load ops from `application.yml` at startup, validate `schema_version`, preload models
- **TaskExecutor** — receive `GPU_TASK_DISPATCH`, call `OpRegistry.handler().execute(input, op_param)`, return `GPU_TASK_RESULT`
- **Isolation tier selection** — MIG (hardware) / MPS (process group) / Soft (single CUDA context)
- **Out-of-band transport** — same-node SHM / cross-node RDMA / NAS / object store

## MVP scope (STORY-2-4)

- Java + Jep (Python bridge)
- 180s default timeout (overridable)
- 1 inference Op: `text_classification`

## v0.5

Split into Java scheduler + Python Sidecar (gRPC) + Rust core.
