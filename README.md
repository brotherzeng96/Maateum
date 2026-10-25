markdown
# ⚖️ Maateum: A Knowledge Verification Protocol for Cognitive Security

[![License: MIT](https://shields.io)](https://opensource.org)
[![Layer: Decentralized Cognitive Layer (DCL)](https://shields.io)](#)
[![Chain-Agnostic](https://shields.io)](#)

> **"Bitcoin eliminated trust in monetary transfer. Ethereum eliminated trust in contract execution. Maateum eliminates trust in decision knowledge."**

Existing blockchain protocols provide cryptographic guarantees over *what* was transacted and *who* signed, but provide **no guarantees over what the signer knew at the moment of decision**. This structural vulnerability—the **Knowledge Gap ($KG$)**—underlies the majority of on-chain fraud, malicious contract exploitation, and AI-generated social engineering attacks.

**Maateum** is a chain-agnostic **Knowledge Verification Protocol (KVP)** operating as a **Decentralized Cognitive Layer (DCL)** above existing execution environments. By enforcing the **Ma'at Condition ($KG = \emptyset$)** prior to transaction execution, Maateum reframes cognitive security from a post-hoc heuristic into a deterministic, protocol-layer cryptographic guarantee.

---

## 📐 1. Problem Formalization: The Knowledge Gap ($KG$)

We formalize a **Decision Event ($D$)** as a 5-tuple:

$$D = \langle \alpha, \mathcal{I}, \tau_{\text{init}}, \tau_{\text{sign}}, \omega \rangle$$

Where $\alpha \in \text{DID}$ is the actor's identifier, $\mathcal{I}$ is the available information set, $\tau_{\text{init}}$ and $\tau_{\text{sign}}$ are timestamps, and $\omega$ is the transaction payload. The **Knowledge Gap ($KG$)** is defined as the set difference against the required information set $\mathcal{I}_{\text{req}}(\omega)$:

$$KG(D) = \mathcal{I}_{\text{req}}(\omega) \setminus \mathcal{I}$$

### Three-Dimensional Decomposition
Maateum decomposes $KG(D)$ into three orthogonal sub-gaps, creating a circuit-breaker defense against specific attack vectors:

$$KG(D) = KG_{\text{id}}(D) \sqcup KG_{\text{int}}(D) \sqcup KG_{\text{hum}}(D)$$

1. **Identity Gap ($KG_{\text{id}}$) $\rightarrow$ Defends Against Blind Spot Attacks (BSA):** Concealing or falsifying counterparty identity.
2. **Integrity Gap ($KG_{\text{int}}$) $\rightarrow$ Defends Against Decision Poisoning Attacks (DPA):** Fiduciary or data modification in transit.
3. **Humanity Gap ($KG_{\text{hum}}$) $\rightarrow$ Defends Against Cognitive Hijack Attacks (CHA):** Deploying malicious AI agents to impersonate human counterparties.

---

## ⚡ 2. The Triple-Proof Core Architecture

Maateum issues a Boolean **Execution Permit ($EP \in \{0, 1\}$)** conditioned on the zero-set state of the Knowledge Gap:

$$EP(D) = PID.\mathit{Verify}(D) \wedge PHD.\mathit{Verify}(D) \wedge POI.\mathit{Verify}(D)$$

請謹慎使用程式碼。
[ User Initiates Transaction TX ]
|
┌─────────────┼─────────────┐
▼             ▼             ▼
┌─────────┐   ┌─────────┐   ┌─────────┐
│   PID   │   │   PHD   │   │   POI   │
│ Proof of│   │ Proof of│   │ Proof of│
│ Informed│   │  Human  │   │  Info   │
│ Decision│   │ Decision│   │Integrity│
└────┬────┘   └────┬────┘   └────┬────┘
│             │             │
└─────────────┼─────────────┘
▼
[ Boolean Execution Permit (EP) ]
├── EP = 1 ──> Execute on-chain
└── EP = 0 ──> Trigger Circuit Breaker & Abort

### 🧠 PID: Proof of Informed Decision
Verifies counterparty reputational thresholds using a time-weighted historical score matrix (\(S_m\)):
\[S_m(did) = \frac{\sum_i e^{-\lambda(\tau - \tau_i)} \cdot b_i}{\sum_i e^{-\lambda(\tau - \tau_i)}}\]

### 🛡️ PHD: Proof of Human Decision
Executes non-interactive behavioral biometric classification (\(B_{\text{vec}}\)) and cognitive challenge responses (\(C_{\text{resp}}\)) inside an hardware-isolated **Trusted Execution Environment (TEE)**, yielding a succinct Zero-Knowledge Proof (**zk-SNARK**) without leaking biometric primitives.
Enforces a **Dynamic Cooling Period (DCP)** constraint:
\[\Delta t \ge DCP(D) = t_{\text{base}} \times f_{\text{risk}}(S_m) \times f_{\text{complex}}(\omega)\]

### 🔍 POI: Proof of Information Integrity
Generates an unforgeable cryptographic anchor matching the source data commitment (\(POI_{\text{root}}\)) via a Merkle Integrity Tree to detect any frontend payload or interface tampering in transit.

---

## 💻 3. Protocol Specifications & Algorithms

Below are the core algorithmic implementations of the Maateum Knowledge Verification Protocol.

### Protocol Verification Pipeline
```python
def verify_protocol_pipeline(D, theta_id, theta_hum):
    """
    Algorithm 1: Maateum.Verify Pipeline Execution
    Evaluates the complete conjunctive protocol above execution environments.
    """
    alpha, I_received, tau_init, tau_sign, omega = D
    did_cp = fetch_counterparty_did(omega)
    
    # 1. Evaluate Identity Proof
    score = get_time_weighted_score(did_cp, tau_sign)
    pid_result = (score >= theta_id)
    
    # 2. Compute Enforced Dynamic Cooling Period
    dcp = compute_dcp(score, omega)
    
    # 3. Evaluate Humanity Proof
    phd_result = verify_humanity_proof(alpha, tau_init, tau_sign, dcp, theta_hum)
    
    # 4. Evaluate Integrity Proof
    poi_root_origin = fetch_onchain_poi_root(omega)
    poi_result = verify_integrity_proof(I_received, poi_root_origin)
    
    # 5. Composite Boolean Permitting Engine
    execution_permit = pid_result and phd_result and poi_result
    
    if execution_permit:
        cert_hash = hash_certificate(D, tau_sign)
        submit_to_settlement_layer(cert_hash, status="APPROVED")
        return True
    else:
        reason_hash = hash_rejection_reason(pid_result, phd_result, poi_result)
        submit_to_settlement_layer(reason_hash, status="ABORTED")
        return False
```

### 🔐 Algorithm 2: Proof of Informed Decision (PID)
```python
import hashlib

def verify_pid(did_cp, score, signature_alpha, public_key_alpha, theta_id, tau_sign):
    """
    Algorithm 2: PID.Verify Engine
    Ensures actor possesses attested information over counterparty bounds.
    """
    if score = {theta_hum}", witness=b_vec)
    return verify_zk_snark_onchain_primitive(zk_proof)
```

---

## 📊 4. Performance & Structural Analysis

### Gas Amortization Architecture (ZK-Rollup Infrastructure)
By computing multi-proof algorithms off-chain within verification nodes running **Proof of Cognitive Validation (PoCV)** consensus and submitting compressed zk-SNARK batches to the settlement tier, on-chain cost reduces by **95–98%** compared to naive on-chain validation.

| Operation Architecture | Estimated EVM Gas | Optimization Mechanics |
| :--- | :--- | :--- |
| Core ECDSA Validation | ~3,000 | `ecrecover` precompile execution |
| PID Attestation & Ledger Commitment | ~25,000 | State serialization primitives (`SSTORE`) |
| Merkle Path Verification (4 tiers) | ~6,000 | Dynamic cryptographic index matching |
| Plonk zk-SNARK Proof Verification | ~200,000 - 600,000 | Complex pair verification overhead |
| **Maateum Naive On-Chain Cost** | **~600,000 - 1,200,000** | Cumulative layer overhead sum |
| **Maateum via ZK-Rollup (Amortized)**| **~2,000 - 5,000** | **Batch-processed structural state compression** |

---

## 📦 5. Developer Quickstart Integration

Maateum integrates via an asynchronous single SDK function compatible with EIP-712 structured data parameters, requiring zero modification to standard infrastructure.

```javascript
import { MaateumSDK } from 'maateum-core';

const executionPermit = await MaateumSDK.verify({
  transaction: eip712TypedDataPayload,
  counterparty: 'did:key:z6MkuV...', // W3C Decentralized Identifier
  chain: 'ethereum'                  // EVM, Arbitrum, or Solana
});

if (executionPermit.EP === true) {
  // Proceed to secure localized transaction signing context
  await wallet.signTransaction(tx);
} else {
  // Trigger localized client circuit breaker interface
  console.error(`Transaction aborted. Reason: ${executionPermit.reasonCode}`);
}
```

## ⚖️ License
This project is licensed under the MIT License - see the LICENSE file for
