# Mainnet Issuance - January xxx, 2025 <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [Documentation](#documentation)
- [URLs \& Versions](#urls--versions)
- [PartyIDs](#partyids)
- [Status](#status)
  - [Step 0: Infrastructure Setup](#step-0-infrastructure-setup)
  - [Step 1: Onboarding roles](#step-1-onboarding-roles)
  - [Step 2: Configuring tokens](#step-2-configuring-tokens)
  - [Step 3: Issuing tokens](#step-3-issuing-tokens)
- [Detailed instructions](#detailed-instructions)
  - [0.1 Setup BR node](#01-setup-br-node)
  - [0.2 Setup SGF node](#02-setup-sgf-node)
  - [0.3 Setup Virtu node](#03-setup-virtu-node)
  - [0.4 Setup DRW node](#04-setup-drw-node)
  - [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities)
  - [1.2 Provider credential](#12-provider-credential)
  - [1.3 Provider onboarding](#13-provider-onboarding)
  - [1.4 Provider configuration](#14-provider-configuration)
  - [1.5 Registrar credential](#15-registrar-credential)
  - [1.6 Registrar onboarding](#16-registrar-onboarding)
  - [2.1 Registrar creates Allocation Factory and Transfer Rule](#21-registrar-creates-allocation-factory-and-transfer-rule)
  - [2.2 Registrar specifies Instrument Configuration](#22-registrar-specifies-instrument-configuration)
    - [EURCV Instrument Configuration](#eurcv-instrument-configuration)
    - [USDCV Instrument Configuration](#usdcv-instrument-configuration)
  - [2.3 Registrar offers credentials to Issuer and Holders](#23-registrar-offers-credentials-to-issuer-and-holders)
    - [Credential to issue EURCV](#credential-to-issue-eurcv)
    - [Credentials to hold EURCV](#credentials-to-hold-eurcv)
    - [Credential to issue USDCV](#credential-to-issue-usdcv)
    - [Credentials to hold USDCV](#credentials-to-hold-usdcv)
  - [3.1 Issuer requests token issuance (minting)](#31-issuer-requests-token-issuance-minting)
    - [EUR10m EURCV minted](#eur10m-eurcv-minted)
    - [USD10m USDCV minted](#usd10m-usdcv-minted)
  - [3.2 Registrar accepts and tokens are minted](#32-registrar-accepts-and-tokens-are-minted)
  - [3.3 Issuer offers token transfer to Virtu](#33-issuer-offers-token-transfer-to-virtu)
    - [EUR10m EURCV minted to Virtu](#eur10m-eurcv-minted-to-virtu)
    - [USD10m USDCV minted to Virtu](#usd10m-usdcv-minted-to-virtu)
  - [3.4 Virtu accepts transfer](#34-virtu-accepts-transfer)

## Documentation

- [Issuing Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/introduction.html)
- [Transfering Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/transfer/index.html)
- [Redeeming Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/redemption/index.html)

## URLs & Versions

| Entity               | Details                                                       | Utility UI version |
| :------------------- | :------------------------------------------------------------ | ------------------ |
| Broadridge (BR)      | https://utility-broadridge.broadridge.catalyst.intellecteu.io | 0.10.16            |
| SG Forge (Registrar) | https://utility-socgen.broadridge.catalyst.intellecteu.io     | 0.10.16            |
| SG Forge (Issuer)    | https://utility-socgen.broadridge.catalyst.intellecteu.io     | 0.10.16            |
| Virtu                | ??                                                            | 0.10.16            |
| DRW                  | ??                                                            | 0.10.16            |

## PartyIDs

| Entity               | Party ID                                                                                                   |
| :------------------- | :--------------------------------------------------------------------------------------------------------- |
| Broadridge           | `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818`                |
| SG Forge (Registrar) | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`                            |
| SG Forge (Issuer)    | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`                     |
| Virtu                | `???`                                                                                                      |
| DRW                  | `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155` |

## Status

### Step 0: Infrastructure Setup

| Steps                                        | IEU  | BR   | SGF  | SGF-Issuer | Virtu | DRW  |
| :------------------------------------------- | :--- | :--- | :--- | :--------- | :---- | :--- |
| [0.1 Setup BR node](#01-setup-br-node)       | ✅    | 📌    | -    | -          | -     | -    |
| [0.2 Setup SGF node](#02-setup-sgf-node)     | ✅    | -    | 📌    | 📌          | -     | -    |
| [0.3 Setup Virtu node](#03-setup-virtu-node) | -    | -    | -    | -          | 📌     | -    |
| [0.4 Setup DRW node](#04-setup-drw-node)     | -    | -    | -    | -          | -     | 📌    |

### Step 1: Onboarding roles

| Steps                                                                                        | DA   | BR   | SGF  | SGF-Issuer | Virtu | DRW  |
| :------------------------------------------------------------------------------------------- | :--- | :--- | :--- | :--------- | :---- | :--- |
| [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities) | -    | 📌    | 📌    | 📌          | 📌     | 📌    |
| [1.2 Provider credential](#12-provider-credential)                                           | 📌    | 📌    | -    | -          | -     | -    |
| [1.3 Provider onboarding](#13-provider-onboarding)                                           | 📌    | 📌    | -    | -          | -     | -    |
| [1.4 Provider configuration](#14-provider-configuration)                                     | -    | 📌    | -    | -          | -     | -    |
| [1.5 Registrar credential](#15-registrar-credential)                                         | -    | 📌    | 📌    | -          | -     | -    |
| [1.6 Registrar onboarding](#16-registrar-onboarding)                                         | -    | 📌    | 📌    | -          | -     | -    |

### Step 2: Configuring tokens

| Steps                                                                                                                    | DA   | BR   | SGF  | SGF-Issuer | Virtu | DRW  |
| :----------------------------------------------------------------------------------------------------------------------- | :--- | :--- | :--- | :--------- | :---- | :--- |
| [2.1 Registrar creates Allocation Factory and Transfer Rule](#21-registrar-creates-allocation-factory-and-transfer-rule) | -    | -    | 📌    | -          | -     | -    |
| [2.2 Registrar specifies Instrument Configuration](#22-registrar-specifies-instrument-configuration)                     | -    | -    | 📌    | -          | -     | -    |
| [2.3 Registrar offers credentials to Issuer and Holders](#23-registrar-offers-credentials-to-issuer-and-holders)         | -    | -    | 📌    | 📌          | 📌     | 📌    |

### Step 3: Issuing tokens

| Steps                                                                                      | DA   | BR   | SGF  | SGF-Issuer | Virtu | DRW  |
| :----------------------------------------------------------------------------------------- | :--- | :--- | :--- | :--------- | :---- | :--- |
| [3.1 Issuer requests token issuance (minting)](#31-issuer-requests-token-issuance-minting) | -    | -    |      | 📌          | -     | -    |
| [3.2 Registrar accepts and tokens are minted](#32-registrar-accepts-and-tokens-are-minted) | -    | -    | 📌    | -          | -     | -    |
| [3.3 Issuer offers token transfer to Virtu](#33-issuer-offers-token-transfer-to-virtu)     | -    | -    | -    | 📌          | -     | -    |
| [3.4 Virtu accepts transfer](#34-virtu-accepts-transfer)                                   | -    | -    | -    | -          | 📌     | -    |

## Detailed instructions

### 0.1 Setup BR node

IEU setup BR node on testnet:

- url: https://utility-broadridge.broadridge.catalyst.intellecteu.io
- DA CN Utility version: 0.10.16
- partyIDs: `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818`
- access credentials shared securely

BR confirms that they are able to access (no IP restriction issues, no firewall issues, no polling issues).

BR turns off `Network Polling` and `Websockets` to avoid potential corporate firewall issues.

![Polling_Websocket_off](images/Polling_Websocket_off.png)

### 0.2 Setup SGF node

IEU setup SGF node on testnet:

- url: https://utility-socgen.broadridge.catalyst.intellecteu.io
- DA CN Utility version: 0.10.16
- partyIDs:
  - `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`
  - `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`
- access credentials shared securely

SGF (Registar) and SGF (Issuer) confirm that they are able to access (no IP restriction issues, no firewall issues).

### 0.3 Setup Virtu node

Virtu setup node on testnet:

- url: ??
- DA CN Utility version: 0.10.16
- partyIDs: `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154`
- access credentials shared securely

Virtu confirms that they are able to access.

### 0.4 Setup DRW node

DRW setup node on testnet:

- url: ??
- DA CN Utility version: 0.10.16
- partyIDs: `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155`
- access credentials shared securely

Virtu confirms that they are able to access.

### 1.1 Credential User Service for all entities

| Actor        | Module     | Tab        |
| :----------- | :--------- | :--------- |
| All entities | Credential | Onboarding |

All entities `Request Credential User Service`.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#onboarding-credential-services-for-all-entities) for details.

### 1.2 Provider credential

| Actors | Module     | Tab                 |
| :----- | :--------- | :------------------ |
| DA, BR | Credential | Credentials, Offers |

DA offers Provider credential (Credentials tab), and BR accepts it (Offers tab):

| Item        | Value                                                                                       |
| :---------- | :------------------------------------------------------------------------------------------ |
| holder      | `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818` |
| id          | `Broadridge provider`                                                                       |
| description | `Broadridge provider`                                                                       |
| Subject     | `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818` |
| Property    | `hasRegistryRole`                                                                           |
| Value       | `Provider`                                                                                  |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#provider-credential) for details.

### 1.3 Provider onboarding

| Actors | Module   | Tab        |
| :----- | :------- | :--------- |
| BR, DA | Registry | Onboarding |

Registrar/Issuer clicks on `Request Provider Service`, and DA accepts it.

DA can refer to this [procedure on how to accept Provider Service requests](https://docs.google.com/document/d/1puEcCTnA0WBs17xiuZdVFEyxKQxYm9UB7DsmSFk4lgQ/edit?tab=t.0#heading=h.aipczhdl5gnn).

### 1.4 Provider configuration

| Actors | Module   | Tab            |
| :----- | :------- | :------------- |
| BR     | Registry | Configurations |

BR creates Provider Configurations: `Required Credentials for Registrars`

| Item              | Value                                                                                       |
| :---------------- | :------------------------------------------------------------------------------------------ |
| credential issuer | `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818` |
| Property          | `hasRegistryRole`                                                                           |
| Value             | `Registrar`                                                                                 |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#registrar-requests-onboarding-as-a-registrar-in-the-registry) for details.

### 1.5 Registrar credential

| Actors                  | Module     | Tab                 |
| :---------------------- | :--------- | :------------------ |
| BR, SG Forge (Registar) | Credential | Credentials, Offers |

BR offers Registrar credential (Credentials tab), and Registrar accepts it (Offers tab):

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| id          | `SG Forge Registrar Credential`                                                 |
| description | `SG Forge Registrar Credential`                                                 |
| Subject     | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property    | `hasRegistryRole`                                                               |
| Value       | `Registrar`                                                                     |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#provider-offers-registrar-credential)for details.

### 1.6 Registrar onboarding

| Actors       | Module   | Tab        |
| :----------- | :------- | :--------- |
| SG Forge, DA | Registry | Onboarding |

Registrar clicks on `Request Registrar Service`, and BR accepts.

| Item     | Value                                                                                       |
| :------- | :------------------------------------------------------------------------------------------ |
| Provider | `broadridge-provider::1220fb5d230808f7caabd740d797daabfc31c7418180e2b1fd2365658f3220edf818` |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#registrar-requests-onboarding-as-a-registrar-in-the-registry) for details.

### 2.1 Registrar creates Allocation Factory and Transfer Rule

| Actors   | Module   | Tab           |
| :------- | :------- | :------------ |
| SG Forge | Registry | Configuration |

Registrar clicks on `Create Allocation Factory` and `Create Transfer Rule`.

Both boxes should turn from blue to grey.

![Allocation Factory Transfer Rule](images/AllocationFactory-TransferRule.png)

### 2.2 Registrar specifies Instrument Configuration

| Actors   | Module   | Tab           |
| :------- | :------- | :------------ |
| SG Forge | Registry | Configuration |

Registrar creates Instrument Configuration:

Instrument Configuration ensures that:

- Only entities with a credential `isIssuerOf=[TOKEN]` from `[REGISTRAR]` can issue `[TOKEN]`
- Only entities with a credential `isHolderOf=[TOKEN]` from `[REGISTRAR]` can hold `[TOKEN]`

> If there is already an `instrument configuration` for these assets, either modify it or archive it before creating a new one.

#### EURCV Instrument Configuration

| Item                        | Value                                                                           |
| :-------------------------- | :------------------------------------------------------------------------------ |
| Instrument ID               | `EURCV`                                                                         |
| Identifiers                 |                                                                                 |
| Source                      | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Id                          | `XT9W5C49FJV7`                                                                  |
| Scheme                      | `ISIN`                                                                          |
| Source                      | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Id                          | `9W5C49FJV`                                                                     |
| Scheme                      | `DTI`                                                                           |
| Requirement for Mint Issuer |                                                                                 |
| Credential Issuer           | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property                    | `isIssuerOf`                                                                    |
| Value                       | `EURCV`                                                                         |
| Requirement for Holders     |                                                                                 |
| Credential Issuer           | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property                    | `isHolderOf`                                                                    |
| Value                       | `EURCV`                                                                         |

#### USDCV Instrument Configuration

| Item                        | Value                                                                           |
| :-------------------------- | :------------------------------------------------------------------------------ |
| Instrument ID               | `USDCV`                                                                         |
| Identifiers                 |                                                                                 |
| Source                      | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Id                          | `XTLD6JM2JN25`                                                                  |
| Scheme                      | `ISIN`                                                                          |
| Source                      | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Id                          | `LD6JM2JN2`                                                                     |
| Scheme                      | `DTI`                                                                           |
| Requirement for Mint Issuer |                                                                                 |
| Credential Issuer           | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property                    | `isIssuerOf`                                                                    |
| Value                       | `USDCV`                                                                         |
| Requirement for Holders     |                                                                                 |
| Credential Issuer           | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property                    | `isHolderOf`                                                                    |
| Value                       | `USDCV`                                                                         |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-specifying-the-requirement-of-the-bond-token) for details.

### 2.3 Registrar offers credentials to Issuer and Holders

| Actors               | Module     | Tab                 |
| :------------------- | :--------- | :------------------ |
| SG Forge, Virtu, DRW | Credential | Credentials, Offers |

Registrar issues free credentials (Credentials tab), and Issuer, Virtu, and DRW accept them (Offers tab).

#### Credential to issue EURCV

| Item        | Value                                                                                  |
| :---------- | :------------------------------------------------------------------------------------- |
| holder      | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| id          | `Issuer-EURCV-Issuer`                                                                  |
| description | `Issuer-EURCV-Issuer`                                                                  |
| Subject     | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property    | `isIssuerOf`                                                                           |
| Value       | `EURCV`                                                                                |

#### Credentials to hold EURCV

| Item        | Value                                                                                  |
| :---------- | :------------------------------------------------------------------------------------- |
| holder      | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| id          | `Issuer-EURCV-Holder`                                                                  |
| description | `Issuer-EURCV-Holder`                                                                  |
| Subject     | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property    | `isHolderOf`                                                                           |
| Value       | `EURCV`                                                                                |

| Item        | Value                                                                                |
| :---------- | :----------------------------------------------------------------------------------- |
| holder      | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| id          | `Virtu-EURCV-Holder`                                                                 |
| description | `Virtu-EURCV-Holder`                                                                 |
| Subject     | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| Property    | `isHolderOf`                                                                         |
| Value       | `EURCV`                                                                              |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155` |
| id          | `DRW-EURCV-Holder`                                                                                         |
| description | `DRW-EURCV-Holder`                                                                                         |
| Subject     | `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `EURCV`                                                                                                    |

#### Credential to issue USDCV

| Item        | Value                                                                                  |
| :---------- | :------------------------------------------------------------------------------------- |
| holder      | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| id          | `Issuer-USDCV-Issuer`                                                                  |
| description | `Issuer-USDCV-Issuer`                                                                  |
| Subject     | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property    | `isIssuerOf`                                                                           |
| Value       | `USDCV`                                                                                |

#### Credentials to hold USDCV

| Item        | Value                                                                                  |
| :---------- | :------------------------------------------------------------------------------------- |
| holder      | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| id          | `Issuer-USDCV-Holder`                                                                  |
| description | `Issuer-USDCV-Holder`                                                                  |
| Subject     | `sgforge-issuer::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Property    | `isHolderOf`                                                                           |
| Value       | `USDCV`                                                                                |

| Item        | Value                                                                                |
| :---------- | :----------------------------------------------------------------------------------- |
| holder      | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| id          | `Virtu-USDCV-Holder`                                                                 |
| description | `Virtu-USDCV-Holder`                                                                 |
| Subject     | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| Property    | `isHolderOf`                                                                         |
| Value       | `USDCV`                                                                              |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155` |
| id          | `DRW-USDCV-Holder`                                                                                         |
| description | `DRW-USDCV-Holder`                                                                                         |
| Subject     | `auth0_007c69121dc70023edf579da8f10::1220f792fc36ceb9f88536e862f0923f1b655cccb9a711ee4d5ede1397ad722bb155` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `USDCV`                                                                                                    |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-offers-credential-of-token-issuer-and-holder-to-issuer) for details.

### 3.1 Issuer requests token issuance (minting)

| Actors     | Module   | Tab   |
| :--------- | :------- | :---- |
| SGF-Issuer | Registry | Mints |

#### EUR10m EURCV minted

| Item       | Value                                                                           |
| :--------- | :------------------------------------------------------------------------------ |
| Instrument | `EURCV`                                                                         |
| Amount     | `10000000`                                                                      |
| Registrar  | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Reference  | `EURCV EUR10m minted xxx-Jan-2026`                                              |

#### USD10m USDCV minted

| Item       | Value                                                                           |
| :--------- | :------------------------------------------------------------------------------ |
| Instrument | `USDCV`                                                                         |
| Amount     | `10000000`                                                                      |
| Registrar  | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1` |
| Reference  | `USDCV USD10m minted xxx-Jan-2026`                                              |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-requests-token-issuance-minting) for details.

### 3.2 Registrar accepts and tokens are minted

| Actors | Module   | Tab   |
| :----- | :------- | :---- |
| SGF    | Registry | Mints |

Registrar accepts and tokens are minted.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#registrar-accepts-and-tokens-are-minted) for details.

### 3.3 Issuer offers token transfer to Virtu

| Actors     | Module   | Tab      |
| :--------- | :------- | :------- |
| SGF-Issuer | Registry | Holdings |

Issuer transfers tokens to Virtu. (3 dots menu on the right of the holding / `Transfer` )

#### EUR10m EURCV minted to Virtu

| Item       | Value                                                                                |
| :--------- | :----------------------------------------------------------------------------------- |
| Send from  | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`      |
| Send to    | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| Instrument | `EURCV`                                                                              |
| Amount     | `10000000`                                                                           |
| Reference  | `EURCV EUR10m minted to Virtu`                                                       |

#### USD10m USDCV minted to Virtu

| Item       | Value                                                                                |
| :--------- | :----------------------------------------------------------------------------------- |
| Send from  | `sgforge::12203e601bb3021da99f2105b460ef92f083faf716377991a636c52b11bda56c6cf1`      |
| Send to    | `virtu-holder::12203e15163301aebdd1bd2e64bbe30f3d794bd70e3419056ca1600c1f3d6370e154` |
| Instrument | `USDCV`                                                                              |
| Amount     | `10000000`                                                                           |
| Reference  | `USDCV USD10m minted to Virtu`                                                       |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-offers-token-transfer-to-Virtu) for details.

### 3.4 Virtu accepts transfer

| Actors | Module   | Tab       |
| :----- | :------- | :-------- |
| Virtu  | Registry | Transfers |

Virtu accepts transfer offer. (click on offer, and then on `Accept`)

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#Virtu-accepts-the-transfer-offer-and-tokens-are-transferred) for details.
