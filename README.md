# 🔐 Decentralized KYC System

**Enterprise-Grade Identity Verification for Fintech & Wealth Management**

> A blockchain-native Know Your Customer (KYC) platform leveraging verifiable credentials, decentralized identifiers (DIDs), and AI-assisted document processing to establish immutable, trustless identity verification for financial institutions.

---

## 📋 Table of Contents

- [Project Vision](#-project-vision)
- [Technical Architecture](#-technical-architecture)
- [Core Features](#-core-features)
- [Smart Contract Overview](#-smart-contract-overview)
- [Technology Stack](#-technology-stack)
- [System Walkthrough](#-system-walkthrough)
- [Deployment Guide](#-deployment-guide)
- [OCR Integration](#-ocr-integration)
- [API Reference](#-api-reference)
- [Future Roadmap](#-future-roadmap)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🎯 Project Vision

### Solving Trust in Digital Identity for Finance

Traditional KYC processes rely on centralized databases vulnerable to breaches, inconsistent verification standards, and friction in cross-institutional identity sharing. This creates operational inefficiencies, regulatory compliance burdens, and identity fraud risks that cost the fintech sector billions annually.

**Decentralized KYC System** addresses these challenges by:

- **Establishing Verifiable Trust**: Credentials issued on-chain are cryptographically signed and immutable, eliminating re-verification cycles
- **Enabling Selective Disclosure**: Users share only the necessary identity attributes required by financial institutions, not entire identity profiles
- **Creating Institutional Interoperability**: DID registries enable seamless credential verification across banks, wealth managers, and fintech platforms
- **Reducing Compliance Friction**: Automated verification workflows for KYC/AML requirements in risk analytics and wealth management operations

This architecture transforms identity from a centralized liability into a decentralized, verifiable asset controlled by users—fundamentally reimagining trust infrastructure for Web3 finance.

---

## 🏗️ Technical Architecture

### System Flow Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                     Decentralized KYC Flow                      │
└─────────────────────────────────────────────────────────────────┘

    ┌──────────────┐         ┌──────────────┐      ┌─────────────┐
    │     User     │         │  Issuer Node │      │   Polygon   │
    │  (Web3)      │         │  (Backend)   │      │   Amoy      │
    └──────────────┘         └──────────────┘      └─────────────┘
          │                         │                      │
          │ 1. Submit DID           │                      │
          │ & Credentials ────────→ │                      │
          │                         │ 2. Verify via       │
          │                         │    OCR Service      │
          │                         │ (Port 8001)         │
          │                         │                      │
          │                         │ 3. Issue Credential │
          │                         │    Smart Contract ──→ DID Registry
          │                         │                      │
          │ ← 4. Receive VCs ───────┤                  Issuer Registry
          │    & Proof               │                  Credential Registry
          │                         │                      │
          │                  ┌──────────────────────────────┘
          │                  │
          │         ┌────────▼──────────┐
          │         │  Financial Portal  │
          │         │  (React Frontend)  │
          │────────→│  Verification UI   │
                    └────────────────────┘


---

## ✨ Core Features

### 1. **Verifiable Credentials (W3C Standard)**
- Cryptographic proof of identity attributes (name, DOB, document hash)
- JWT/JSON-LD formatted credentials issued by trusted institutions
- Selective disclosure: Users prove attributes without revealing underlying data

### 2. **Decentralized Identifier (DID) Registry**
- Self-sovereign identity model on Polygon Amoy
- User-controlled DID document with public keys
- Supports document recovery and key rotation

### 3. **AI-Assisted Document Verification**
- Python OCR service (port 8001) processes identity documents
- Extracts structured data: Name, DOB, Document Type, Expiry Date
- Integrates with automated verification workflows

### 4. **Institutional Interoperability**
- Issuer registry for trusted credential issuers
- One-time verification, unlimited institutional reuse
- Reduces KYC/AML friction across fintech ecosystems

### 5. **Risk Analytics Integration**
- Credential-based risk scoring for wealth management platforms
- Compliance audit trails for regulatory reporting
- Real-time credential status verification

---

## 🔧 Smart Contract Overview

### **Issuer Registry Smart Contract**
```solidity
// Contract: IssuerRegistry.sol
// Purpose: Maintain registry of trusted KYC issuers
// Key Functions:
// - registerIssuer(address, metadata): Register new issuer
// - revokeIssuer(address): Deactivate compromised issuer
// - isIssuerValid(address): Check issuer status
```

### **DID Registry Smart Contract**
```solidity
// Contract: DIDRegistry.sol
// Purpose: Store decentralized identifiers and their documents
// Key Functions:
// - registerDID(string memory did, document): Create user identity
// - updateDIDDocument(string memory did, newDoc): Rotate keys
// - resolveDID(string memory did): Retrieve DID document
// - revokeDID(string memory did): Deactivate identity (user initiated)
```

### **Credential Registry Smart Contract**
```solidity
// Contract: CredentialRegistry.sol
// Purpose: Issue, verify, and revoke verifiable credentials
// Key Functions:
// - issueCredential(did, attributes[], issuer): Mint credential
// - verifyCredential(credentialId): Validate credential authenticity
// - revokeCredential(credentialId, reason): Revoke compromised credential
// - getCredentialStatus(credentialId): Check revocation status
```

**Network**: Polygon Amoy Testnet  
**Solidity Version**: 0.8.30  
**Consensus**: Proof-of-Stake

---

## 🛠️ Technology Stack

| Component | Technology | Version | Purpose |
|-----------|-----------|---------|---------|
| **Blockchain** | Polygon Amoy | - | EVM-compatible testnet for smart contracts |
| **Smart Contracts** | Solidity | 0.8.30 | DID, Issuer, and Credential registries |
| **Dev Framework** | Hardhat | Latest | Smart contract compilation, testing, deployment |
| **Frontend** | React 18+ | - | User dashboard and credential management UI |
| **Backend** | Node.js | 18+ | REST API, credential issuance logic |
| **Document Processing** | Python (OCR) | 3.9+ | Document extraction and verification service |
| **OCR Engine** | Tesseract/EasyOCR | - | Runs on port 8001 |
| **Web3 Integration** | ethers.js | Latest | Blockchain interaction from frontend |

---

## 📸 System Walkthrough

### **Step 1: User ID Registration**

![User Registration Flow](https://via.placeholder.com/800x400?text=User+ID+Registration+Placeholder)

<img width="1600" height="812" alt="PHOTO-2026-05-12-22-54-44" src="https://github.com/user-attachments/assets/edf03a05-1a25-4564-897e-6e0414d0ea56" />

**User Actions:**
1. Create unique DID (did:polygon:amoy:...)
2. Upload identity document (Passport, Driver License, National ID)
3. System extracts metadata via OCR service
4. User confirms extracted information

---

### **Step 2: MetaMask Connection & Consent**

![MetaMask Integration](https://via.placeholder.com/800x400?text=MetaMask+Connection+Placeholder)
<img width="1435" height="699" alt="Screenshot 2026-05-12 at 2 47 57 AM" src="https://github.com/user-attachments/assets/1c1f1277-2f99-420b-92b0-880486c4ac5f" />

<img width="1435" height="898" alt="Screenshot 2026-05-12 at 2 50 24 AM" src="https://github.com/user-attachments/assets/2eb21d9e-c771-425f-a6ef-832fa81f3bed" />
<img width="1435" height="898" alt="Screenshot 2026-05-12 at 2 50 42 AM" src="https://github.com/user-attachments/assets/3608f63e-b8a4-4ee8-8287-62abd2be4aa2" />

<img width="1435" height="898" alt="Screenshot 2026-05-12 at 2 51 14 AM" src="https://github.com/user-attachments/assets/ac18da29-d44c-46c1-9000-2d51d038251c" />



**Technical Flow:**
1. Frontend prompts user to connect MetaMask wallet
2. Smart contract validates wallet ownership
3. User signs credential issuance transaction
4. Backend broadcasts transaction to Polygon Amoy
5. Credential minted in CredentialRegistry with user's DID

---

### **Step 3: Credential Dashboard UI**

![Credential Management](https://via.placeholder.com/800x400?text=Credential+Dashboard+Placeholder)

<img width="1600" height="791" alt="PHOTO-2026-05-12-22-55-07" src="https://github.com/user-attachments/assets/90a3dd39-b636-4512-afef-15caea7fafaf" />


**Features:**
- View all issued verifiable credentials
- Export credentials in JSON-LD format
- Share selective attributes with institutions
- Revocation history and audit logs
- Credential expiry management

---

## 🚀 Deployment Guide

### **Prerequisites**

```bash
# Node.js 18+ and npm
node --version  # v18.0.0 or higher
npm --version   # v9.0.0 or higher

# Hardhat installation
npm install -g hardhat

# MetaMask or Web3 wallet with Polygon Amoy testnet configured
# Get testnet MATIC from: https://faucet.polygon.technology/
```

### **Step 1: Environment Configuration**

Create `.env` file in project root:

```env
# Polygon Amoy RPC
POLYGON_AMOY_RPC_URL=https://rpc-amoy.polygon.technology/

# Private key (remove 0x prefix)
PRIVATE_KEY=your_wallet_private_key_without_0x

# Smart contract deployment addresses (post-deployment)
ISSUER_REGISTRY_ADDRESS=0x...
DID_REGISTRY_ADDRESS=0x...
CREDENTIAL_REGISTRY_ADDRESS=0x...

# API Configuration
ISSUER_BACKEND_URL=http://localhost:3001
OCR_SERVICE_URL=http://localhost:8001
```

### **Step 2: Smart Contract Compilation**

```bash
# Navigate to contracts directory
cd contracts

# Compile Solidity contracts (0.8.30)
npx hardhat compile

# Output
# Compiled 3 contracts successfully

# Run tests (optional but recommended)
npx hardhat test
```

### **Step 3: Deploy to Polygon Amoy**

```bash
# Deploy using Hardhat deployment script
npx hardhat run scripts/deploy.js --network polygon-amoy

# Expected Output:
# IssuerRegistry deployed to: 0x1234...
# DIDRegistry deployed to: 0x5678...
# CredentialRegistry deployed to: 0x9abc...
```

### **Step 4: Backend API Server (Node.js)**

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Environment variables for backend
# Create .env with POLYGON_AMOY_RPC_URL, smart contract addresses

# Start backend server (port 3001)
npm start

# Console output:
# Server running on http://localhost:3001
# Connected to Polygon Amoy RPC
```

### **Step 5: OCR Service Deployment (Python)**

```bash
# Navigate to OCR service directory
cd ocr-service

# Create Python virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Start OCR service (port 8001)
python app.py

# Console output:
# OCR Service running on http://localhost:8001
# Ready to process documents
```

### **Step 6: Frontend Deployment (React)**

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Build production bundle
npm run build

# Start development server (port 3000)
npm start

# Application available at http://localhost:3000
# Ensure MetaMask is connected to Polygon Amoy
```

### **V2 API Verification**

Verify all services are operational:

```bash
# Test Polygon Amoy connectivity
curl https://rpc-amoy.polygon.technology/ \
  -X POST \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"eth_chainId","params":[],"id":1}'

# Expected Response: {"result":"0x13881"} (Amoy Chain ID)

# Test Backend API health
curl http://localhost:3001/health

# Response: {"status":"ok","network":"polygon-amoy"}

# Test OCR Service
curl -X POST http://localhost:8001/ocr \
  -F "document=@sample_passport.jpg"

# Response: {"extracted_text":"John Doe, DOB: 1990-01-15..."}
```

---

## 🤖 OCR Integration

### **Architecture**

The Python OCR service operates as a microservice, decoupled from backend logic:

```
┌────────────────────────────────────────────────────────┐
│              Document Processing Pipeline              │
└────────────────────────────────────────────────────────┘

User Upload
    ↓
[Frontend - React] 
    ↓ (multipart/form-data)
[Backend API - Node.js] (Port 3001)
    ↓ (forward request)
[OCR Service - Python] (Port 8001)
    │
    ├─ Image Preprocessing (deskew, enhance)
    ├─ Tesseract/EasyOCR Processing
    ├─ NLP-based Field Extraction (Name, DOB, Doc Type)
    ├─ Validation & Confidence Scoring
    │
    ↓ (return JSON)
[Backend - Validation Logic]
    │
    ├─ Cross-reference with issuer databases
    ├─ Liveness detection (optional)
    ├─ Fraud detection scoring
    │
    ↓ (on success)
[Smart Contract - CredentialRegistry]
    │
    └─ Issue Verifiable Credential to User DID
```

### **Supported Document Types**

| Document Type | Fields Extracted | Validation Rules |
|---|---|---|
| **Passport** | Name, DOB, Nationality, Expiry, MRZ | MRZ checksum validation |
| **Driver License** | Name, DOB, Address, DL #, Class | Format validation per jurisdiction |
| **National ID** | Name, DOB, ID Number, Issue/Expiry | RFID/chip validation (if equipped) |
| **Visa/Travel Doc** | Name, DOB, Visa Type, Validity | VFS/Embassy cross-check possible |

### **OCR Service Endpoints**

#### `POST /ocr/extract`
Extract structured data from uploaded document

**Request:**
```bash
curl -X POST http://localhost:8001/ocr/extract \
  -F "document=@passport.jpg" \
  -F "doc_type=passport"
```

**Response:**
```json
{
  "status": "success",
  "confidence": 0.96,
  "extracted_data": {
    "name": "Jane Doe",
    "date_of_birth": "1990-05-15",
    "document_type": "passport",
    "document_number": "AB123456",
    "expiry_date": "2028-06-20",
    "nationality": "USA",
    "mrz_valid": true
  },
  "processing_time_ms": 342
}
```

#### `POST /ocr/verify`
Verify document authenticity using ML-based fraud detection

**Request:**
```json
{
  "document_image": "base64_encoded_image",
  "extracted_data": { ... }
}
```

**Response:**
```json
{
  "authentic": true,
  "fraud_score": 0.08,
  "warnings": [],
  "verification_timestamp": "2026-05-13T10:30:00Z"
}
```

### **Integration Points**

1. **Frontend**: Sends document image to Backend API
2. **Backend**: Forwards to OCR Service, receives structured data
3. **Validation Layer**: Cross-references with issuer databases, applies business rules
4. **Smart Contract**: Issues credential upon successful verification

---

## 📡 API Reference

### **Backend API (Node.js, Port 3001)**

#### **Credential Endpoints**

```http
POST /api/v1/credentials/issue
Content-Type: application/json

{
  "did": "did:polygon:amoy:0x1234...",
  "issuer_did": "did:polygon:amoy:issuer:0x5678...",
  "attributes": {
    "name": "Jane Doe",
    "date_of_birth": "1990-05-15",
    "document_hash": "0xabcd..."
  },
  "expires_in_days": 365
}

Response 201:
{
  "credential_id": "cred_1234567890abcdef",
  "transaction_hash": "0x...",
  "status": "issued",
  "credential_json": { ... }
}
```

#### **DID Endpoints**

```http
POST /api/v1/did/register
Content-Type: application/json

{
  "wallet_address": "0x1234...",
  "public_key": "0x5678...",
  "metadata": {
    "name": "Jane Doe",
    "email": "jane@example.com"
  }
}

Response 201:
{
  "did": "did:polygon:amoy:0x1234...",
  "transaction_hash": "0x...",
  "created_at": "2026-05-13T10:30:00Z"
}
```

#### **Verification Endpoints**

```http
GET /api/v1/verify/credential/:credential_id

Response 200:
{
  "valid": true,
  "issuer": "did:polygon:amoy:issuer:0x5678...",
  "subject": "did:polygon:amoy:0x1234...",
  "revoked": false,
  "expiry": "2027-05-13T10:30:00Z"
}
```

---

## 🗺️ Future Roadmap

### **Phase 1: Foundation (Q3 2026)**
- ✅ Core DID & Credential Registries
- ✅ Basic OCR Integration
- ✅ MetaMask Wallet Integration
- **In Progress**: Polygon Amoy Testnet Deployment

### **Phase 2: Enterprise Features (Q4 2026)**
- 🔄 Multi-Chain Support (Ethereum, Base, Arbitrum)
- 🔄 Advanced Fraud Detection (Biometric Liveness, Document Tampering)
- 🔄 Compliance Reporting (AML/CTF, Sanctions Screening)
- 🔄 Institutional Dashboard (Bank Risk Analytics)

### **Phase 3: Scale & Governance (Q1 2027)**
- 🔄 Decentralized Issuer Governance (DAO)
- 🔄 Zero-Knowledge Proof Integration (Enhanced Privacy)
- 🔄 Mainnet Deployment (Polygon, Ethereum)
- 🔄 API Rate Limiting & Enterprise Tier

### **Phase 4: Ecosystem Integration (Q2 2027)**
- 🔄 SWIFT Integration (Legacy Banking)
- 🔄 Uniswap Flash Loan Support (DeFi Credit Assessment)
- 🔄 Real-World Asset (RWA) Tokenization
- 🔄 Cross-Border Payment Pre-KYC

---

## 🤝 Contributing

We welcome contributions from blockchain engineers, fintech developers, and KYC/AML specialists.

### **Development Workflow**

1. Fork repository
2. Create feature branch: `git checkout -b feature/your-feature`
3. Commit changes: `git commit -m "feat: add feature"`
4. Push to branch: `git push origin feature/your-feature`
5. Open Pull Request with detailed description

### **Code Standards**

- **Solidity**: Follow Solidity Style Guide (0.8.30)
- **JavaScript**: ESLint + Prettier configuration included
- **Python**: PEP 8 compliance, type hints required

### **Testing Requirements**

```bash
# Solidity tests
npx hardhat test

# Backend tests
npm test

# Frontend tests
npm run test:ui
```

---

## 📄 License

MIT License - See [LICENSE](./LICENSE) file for details

**Copyright © 2026 Decentralized KYC System Contributors**

---

## 📞 Support & Contact

- **Issues**: [GitHub Issues](https://github.com/BEGINNERUSER-git/Decentralized-KYC-System/issues)
- **Documentation**: [Full Docs](./docs/README.md)
- **Security**: For vulnerabilities, email security@example.com (do NOT open public issues)

---

## 🙏 Acknowledgments

- **Polygon Labs** - Infrastructure & testnet support
- **W3C Credentials Community Group** - Standards & specifications

---

**Built with ❤️ for the future of decentralized finance** 🚀

---

## Quick Links

| Resource | Link |
|----------|------|
| **Polygon Amoy Faucet** | https://faucet.polygon.technology/ |
| **Smart Contract Explorer** | https://amoy.polygonscan.com/ |
| **W3C Verifiable Credentials** | https://www.w3.org/TR/vc-data-model/ |
| **Hardhat Documentation** | https://hardhat.org/docs |
| **Tesseract OCR** | https://github.com/UB-Mannheim/tesseract |




https://github.com/user-attachments/assets/05c136b4-6273-486a-bc89-0bd0a9518ab6

## Live Demo
https://decentralized-kyc-system-two.vercel.app/login

\


