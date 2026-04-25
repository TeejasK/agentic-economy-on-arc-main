# Agent-to-Agent Marketplace on Arc

**Author:** TEEJAS K  
**Location:** Chennai, Tamil Nadu, India  

This repository contains the **Web UI implementation** for an Agent-to-Agent (A2A) marketplace built as part of the **Agentic Economy on Arc Hackathon**.

**Track:** Agent-to-Agent Payment Loop  

---

## Project Overview

This project demonstrates how autonomous AI agents can:

- Discover and evaluate services from other agents  
- Select optimal providers using price, performance, and reputation  
- Execute tasks and exchange value in **sub-cent USDC payments**  
- Record trust and feedback on-chain using Arc (ERC-8004 reputation)  

The system highlights a key idea:  
**agent-to-agent economies become viable only when transaction costs are extremely low.**

---

## Repository Structure

To simplify deployment and scalability, the system is split into two repositories:

| Component | Repository | Deployment |
|----------|-----------|-----------|
| Web Interface | https://github.com/TEEJASK/agentic-economy-on-arc | Vercel |
| Backend (A2A Engine) | https://github.com/TEEJASK/agentic-economy-on-arc-backend | Railway |

> If only one repository is required for submission, use the Web UI repo and reference the backend in the README.

---

## System Capabilities

- **Requester Agent**
  - Receives user tasks and initiates workflow  

- **Broker Agents**
  - Provide paid services (e.g., sentiment analysis, summarization, pricing data)  

- **Smart Selection Logic**
  - Chooses brokers based on:
    - Cost efficiency  
    - Service relevance  
    - Reputation score  

- **Micro-Payment Execution**
  - Each action is paid using USDC (as low as $0.002)  
  - Powered by Circle Nanopayments (x402 protocol)  

- **Judge Agent**
  - Evaluates output quality  
  - Assigns a performance score  

- **On-Chain Reputation**
  - Feedback is written to Arc blockchain  
  - Enables trust-based future selection  

- **Throughput Demonstration**
  - Includes a 50-transaction test run  
  - Validates scalability and real-time performance  

---

## Hackathon Requirement Alignment

| Requirement | Implementation |
|------------|--------------|
| Sub-cent per-action pricing | $0.002 – $0.008 per call |
| 50+ transactions | Dedicated 50-Tx proof run in UI |
| Circle integration | Wallets + x402 + Nanopayments |
| Arc blockchain usage | Reputation feedback + transaction logs |
| Economic feasibility | Explained in margin analysis |
| Product feedback | Included in documentation |

---

## System Architecture

```mermaid
flowchart LR
  User["User"] --> Web["Next.js Web UI (Vercel)"]
  Web --> Backend["FastAPI Backend (Railway)"]

  subgraph BackendFlow
    Backend --> Profiler["Task Profiler (AI Model)"]
    Backend --> Requester["Requester Agent"]
    Backend --> Brokers["Broker Agents"]
    Backend --> Judge["Judge Agent"]
  end

  Requester --> Payments["Circle x402 Payments"]
  Payments --> Brokers
  Judge --> Chain["Arc Blockchain (Reputation)"]
  Backend --> Web