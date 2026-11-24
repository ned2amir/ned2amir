# [Amir.M]

### Fullstack IoT Platform Engineer
**React/Vite · Django/DRF · JWT · Redis · Linux headless · AVR/ATmega16 · Lichee Pi**

I design and operate end-to-end IoT platforms: operator-facing interfaces, authenticated API surfaces, persistence and caching layers, headless deployment topology, and the firmware that terminates the physical loop. My work is scoped by interface contracts and verified by commit hash — not by verbal assurance.

---

## 🧱 Architecture I Actually Implement

### Frontend
- **React + Vite** SPA with route-level code splitting; state isolated from transport layer so API contract changes don't cascade into view logic.
- **PyQt** desktop clients for operator tooling where browser sandboxing is a constraint (serial access, local device enumeration).
- **Injection surface control:** output encoding at render boundary, CSP headers set at reverse proxy, no string-concatenated SQL anywhere — parameterized queries only. Input validated at API boundary *and* UI boundary (defense in depth, not redundancy).
- **Bottleneck profiling:** render-blocking asset audit, bundle analysis, memoization where re-render cost is measurable — not speculative.

### Backend
- **Django + DRF** with explicit serializer boundaries; business logic kept out of views so the API is testable without HTTP.
- **JWT:** short-lived access tokens, rotating refresh tokens, revocation list in Redis. Token validation is middleware, not per-view boilerplate.
- **Persistence:** SQLite for single-node/dev parity, PostgreSQL for concurrent write paths — migration strategy defined *before* the first model, not after.
- **Redis:** cache-aside for read-heavy endpoints, queue brokering for async ingest, session/revocation store. Hit-rate and eviction policy are monitored, not assumed.
- **Query discipline:** `select_related`/`prefetch_related` on N+1 paths, `EXPLAIN` before index decisions, connection pooling configured against actual concurrency.

### Embedded
- **AVR / ATmega16** in C++: register-level peripheral configuration, interrupt-driven sensor sampling, deterministic control loop timing.
- **Lichee Pi** for Linux-capable edge nodes: cross-compiled binaries, device tree awareness, serial/GPIO boundary to the Django ingest layer.
- **Full-system integration:** built and operated a soccer robot end-to-end — sensor acquisition, control loop, actuation, comms. The integration failure modes (timing jitter, bus contention, power brownout) are ones I've debugged on hardware, not simulated.

### Deployment / Ops
- **Headless Linux:** systemd unit definitions with restart policies and dependency ordering, reverse proxy termination, firewall rules, SSH key-only auth, log rotation, least-privilege service users per unit.
- **Selenium + driver management:** pinned driver versions, headless Chrome flags, explicit waits over sleeps — automation that doesn't rot on driver updates.
- **Data pipelines:** bs4 DOM traversal + regex normalization, with schema validation at ingest so malformed upstream HTML fails loudly instead of silently poisoning the store.

---

## 💼 Engagement Models — Priced on Integration Risk

I price on **verifiable outcome**, not elapsed time. The model is chosen by where the risk actually sits.

### Full Payment — Fixed Platform Delivery
**Applicable when:** interface contracts (API schema, device protocol, deploy target) are locked before work starts.  
**Rationale:** integration risk is mine. I've absorbed firmware-to-dashboard integration before; the "works on my machine" class of failure is priced in, not discovered later. Delivery verified against commit hash and a working demo on the target headless host.

### 50% Upfront / 50% on Verified Delivery — Hardware-in-Loop
**Applicable when:** flashing, wiring, field calibration, or device enumeration is in scope.  
**Rationale:** hardware state is not reversible — a mis-flashed ATmega16 or a mis-wired Lichee Pi node is a real cost. Upfront commits both sides; backend releases on **verified commit hash + reproducible demo**, not verbal sign-off.

### Settlement — USDT / USDC
Invoiced in USD, settled in stablecoin. **Network confirmed in writing before transfer** (TRC-20 vs ERC-20 vs Polygon) — cross-network sends are unrecoverable and are the single most common crypto payment failure. For IoT retainers this also decouples payment confirmation from deploy windows.

> **Case reference:** Django + React sensor platform on headless Linux VPS. DRF API with JWT rotation, Redis cache-aside on read paths, systemd units with restart policy, SSH hardened to key-only, Vite dashboard with CSP set at proxy. Fixed scope → full payment. Verified on commit hash. No renegotiation.

---

## 🔭 Active Work
- **Ingest pipeline:** AVR → serial framing → Django ingest → Redis queue → React live view. Latency profiled at each hop; backpressure handled at the queue, not the UI.
- **Headless automation harness:** Selenium with pinned drivers, regex-normalized output, schema-validated on ingest.

## 🛠️ Stack
`React` · `Vite` · `PyQt` · `HTML/CSS` · `Django` · `DRF` · `JWT` · `SQLite` · `PostgreSQL` · `Redis` · `Linux (headless)` · `systemd` · `Selenium` · `bs4` · `regex` · `C++` · `AVR / ATmega16` · `Lichee Pi`

**Security posture:** parameterized queries, CSP at proxy, JWT rotation + Redis revocation, input validation at API and UI boundaries, key-only SSH, per-unit least-privilege service users.

## 📫 Engage
- **Project inquiry:** [email] — subject `IoT Platform — [scope]`
- **Paid consult:** [Buy Me a Coffee] — architecture review, credited toward engagement if we proceed.

---

## ☕ Support / Hire

<a href="https://www.buymeacoffee.com/YOUR_USERNAME" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 50px !important;width: 180px !important;" ></a>
**Crypto — project payments only; email for invoice first:**
- **USDT (BEP20):** `0x5d36df8f9808895c8f79f5ae60ce6f9e5faf7fc5`
- **USDC (Polygon):** `0x2f280b7c014e010b8e528003e1a2f2eb04fbfedc`
  [Please confirm the network with me before sending; cross-network transfers will result in permanent loss.]

