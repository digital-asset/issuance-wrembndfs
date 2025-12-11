# Testnet Issuance #1 - December xxx, 2025 <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [Documentation](#documentation)
- [URLs \& Versions](#urls--versions)
- [PartyIDs](#partyids)
- [Status](#status)
  - [Step 1: Onboarding roles](#step-1-onboarding-roles)
  - [Step 2: Configuring tokens](#step-2-configuring-tokens)
  - [Step 3: Issuing tokens](#step-3-issuing-tokens)
  - [Step 4: Transfering tokens](#step-4-transfering-tokens)
- [Detailed instructions](#detailed-instructions)
  - [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities)
  - [1.2 Registrar credential](#12-registrar-credential)
  - [1.3 Registrar onboarding](#13-registrar-onboarding)
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
    - [EUR10m EURCV issued](#eur10m-eurcv-issued)
    - [USD10m USDCV issued](#usd10m-usdcv-issued)
  - [3.2 Registrar accepts and tokens are issued](#32-registrar-accepts-and-tokens-are-issued)
  - [3.3 Issuer offers token transfer to Investor1](#33-issuer-offers-token-transfer-to-investor1)
    - [EUR8m EURCV placed to Investor1](#eur8m-eurcv-placed-to-investor1)
    - [USD8m USDCV placed to Investor1](#usd8m-usdcv-placed-to-investor1)
  - [3.4 Investor1 accepts transfer](#34-investor1-accepts-transfer)
  - [4.1 Investor1 offers token transfer to Investor2](#41-investor1-offers-token-transfer-to-investor2)
    - [EUR3m EURCV transfer from Investor1 to Investor2](#eur3m-eurcv-transfer-from-investor1-to-investor2)
    - [USD3m USDCV transfer from Investor1 to Investor2](#usd3m-usdcv-transfer-from-investor1-to-investor2)
  - [4.2 Investor2 accepts transfer](#42-investor2-accepts-transfer)
- [Test 'freeze asset' feature](#test-freeze-asset-feature)

## Documentation

- [Issuing Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/introduction.html)
- [Transfering Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/transfer/index.html)
- [Redeeming Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/redemption/index.html)

## URLs & Versions

| Entity               | Details                                                                                 | Utility UI version |
| :------------------- | :-------------------------------------------------------------------------------------- | ------------------ |
| SG Forge (Registrar) | https://utility-socgen.test.broadridge.catalyst.intellecteu.io                          | 0.9.3              |
| SG Forge (Issuer)    | https://utility-socgen.test.broadridge.catalyst.intellecteu.io                          | 0.9.3              |
| Investor1            | https://validator-pool-001-utility.utility.cnu.testnet.da-int.net/credential/onboarding | 0.10.2             |
| Investor2            | https://validator-pool-001-utility.utility.cnu.testnet.da-int.net/credential/onboarding | 0.10.2             |

## PartyIDs

| Entity               | Party ID                                                                                                   |
| :------------------- | :--------------------------------------------------------------------------------------------------------- |
| SG Forge (Registrar) | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3`                            |
| SG Forge (Issuer)    | `sgforge-issuer::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3`                     |
| Investor1            | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Investor2            | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |

## Status

### Step 1: Onboarding roles

| Steps                                                                                        | DA   | SG Forge (Registrar) | SG Forge (Issuer) | Investor1 | Investor2 |
| :------------------------------------------------------------------------------------------- | :--- | :------------------- | :---------------- | :-------- | :-------- |
| [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities) | -    | ✅                    | 📌                 | ✅         | ✅         |
| [1.2 Registrar credential](#12-registrar-credential)                                         | ✅    | ✅                    | 📌                 | -         | -         |
| [1.3 Registrar onboarding](#13-registrar-onboarding)                                         | ✅    | ✅                    | 📌                 | -         | -         |

### Step 2: Configuring tokens

| Steps                                                                                                                    | DA   | SG Forge | Investor1 | Investor2 |
| :----------------------------------------------------------------------------------------------------------------------- | :--- | :------- | :-------- | :-------- |
| [2.1 Registrar creates Allocation Factory and Transfer Rule](#21-registrar-creates-allocation-factory-and-transfer-rule) | -    | ✅        | -         | -         |
| [2.2 Registrar specifies Instrument Configuration](#22-registrar-specifies-instrument-configuration)                     | -    | 📌        | -         | -         |
| [2.3 Registrar offers credentials to Issuer and Holders](#23-registrar-offers-credentials-to-issuer-and-holders)         | -    | 📌        | 📌         | 📌         |

### Step 3: Issuing tokens

| Steps                                                                                          | DA   | SG Forge | Investor1 | Investor2 |
| :--------------------------------------------------------------------------------------------- | :--- | :------- | :-------- | :-------- |
| [3.1 Issuer requests token issuance (minting)](#31-issuer-requests-token-issuance-minting)     | -    | 📌        | -         | -         |
| [3.2 Registrar accepts and tokens are issued](#32-registrar-accepts-and-tokens-are-issued)     | -    | 📌        | -         | -         |
| [3.3 Issuer offers token transfer to Investor1](#33-issuer-offers-token-transfer-to-investor1) | -    | 📌        | -         | -         |
| [3.4 Investor1 accepts transfer](#34-investor1-accepts-transfer)                               | -    | -        | 📌         | -         |

### Step 4: Transfering tokens

| Steps                                                                                                | DA   | SG Forge | Investor1 | Investor2 |
| :--------------------------------------------------------------------------------------------------- | :--- | :------- | :-------- | :-------- |
| [4.1 Investor1 offers token transfer to Investor2](#41-investor1-offers-token-transfer-to-investor2) | -    | -        | 📌         | -         |
| [4.2 Investor2 accepts transfer](#42-investor2-accepts-transfer)                                     | -    | -        | -         | 📌         |

## Detailed instructions

### 1.1 Credential User Service for all entities

| Actor        | Module     | Tab        |
| :----------- | :--------- | :--------- |
| All entities | Credential | Onboarding |

All entities `Request Credential User Service`.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#onboarding-credential-services-for-all-entities) for details.

### 1.2 Registrar credential

| Actors                | Module     | Tab                 |
| :-------------------- | :--------- | :------------------ |
| DA, Registar / Issuer | Credential | Credentials, Offers |

DA offers Registrar credential (Credentials tab), and Registrar accepts it (Offers tab):

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `SG Forge Registrar Credential`                                                 |
| description | `SG Forge Registrar Credential`                                                 |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `hasRegistryRole`                                                               |
| Value       | `Registrar`                                                                     |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#provider-offers-registrar-credential)for details.

### 1.3 Registrar onboarding

| Actors       | Module   | Tab        |
| :----------- | :------- | :--------- |
| SG Forge, DA | Registry | Onboarding |

Registrar clicks on `Request Registrar Service`, and DA accepts.

| Item     | Value                                                                                                |
| :------- | :--------------------------------------------------------------------------------------------------- |
| Provider | `DigitalAsset-UtilityOperator::12202679f2bbe57d8cba9ef3cee847ac8239df0877105ab1f01a77d47477fdce1204` |

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

#### EURCV Instrument Configuration

| Item                        | Value                                                                           |
| :-------------------------- | :------------------------------------------------------------------------------ |
| Instrument ID               | `EURCV-TESTNET`                                                                 |
| Identifiers                 |                                                                                 |
| Source                      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Id                          | `XT9W5C49FJV7`                                                                  |
| Scheme                      | `ISIN`                                                                          |
| Source                      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Id                          | `9W5C49FJV`                                                                     |
| Scheme                      | `DTI`                                                                           |
| Requirement for Mint Issuer |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isIssuerOf`                                                                    |
| Value                       | `EURCV`                                                                         |
| Requirement for Holders     |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isHolderOf`                                                                    |
| Value                       | `EURCV`                                                                         |

#### USDCV Instrument Configuration

| Item                        | Value                                                                           |
| :-------------------------- | :------------------------------------------------------------------------------ |
| Instrument ID               | `USDCV-TESTNET`                                                                 |
| Identifiers                 |                                                                                 |
| Source                      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Id                          | `XTLD6JM2JN25`                                                                  |
| Scheme                      | `ISIN`                                                                          |
| Source                      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Id                          | `LD6JM2JN2`                                                                     |
| Scheme                      | `DTI`                                                                           |
| Requirement for Mint Issuer |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isIssuerOf`                                                                    |
| Value                       | `USDCV`                                                                         |
| Requirement for Holders     |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isHolderOf`                                                                    |
| Value                       | `USDCV`                                                                         |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-specifying-the-requirement-of-the-bond-token) for details.

### 2.3 Registrar offers credentials to Issuer and Holders

| Actors                         | Module     | Tab                 |
| :----------------------------- | :--------- | :------------------ |
| SG Forge, Investor1, Investor2 | Credential | Credentials, Offers |

Registrar issues free credentials (Credentials tab), and Issuer, Investor1, and Investor2 accept them (Offers tab).

#### Credential to issue EURCV

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `Issuer-EURCV-Issuer`                                                           |
| description | `Issuer-EURCV-Issuer`                                                           |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isIssuerOf`                                                                    |
| Value       | `EURCV`                                                                         |

#### Credentials to hold EURCV

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `Issuer-EURCV-Holder`                                                           |
| description | `Issuer-EURCV-Holder`                                                           |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isHolderOf`                                                                    |
| Value       | `EURCV`                                                                         |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| id          | `Investor1-EURCV-Holder`                                                                                   |
| description | `Investor1-EURCV-Holder`                                                                                   |
| Subject     | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `EURCV`                                                                                                    |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| id          | `Investor2-EURCV-Holder`                                                                                   |
| description | `Investor2-EURCV-Holder`                                                                                   |
| Subject     | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `EURCV`                                                                                                    |

#### Credential to issue USDCV

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `Issuer-USDCV-Issuer`                                                           |
| description | `Issuer-USDCV-Issuer`                                                           |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isIssuerOf`                                                                    |
| Value       | `USDCV`                                                                         |

#### Credentials to hold USDCV

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `Issuer-USDCV-Holder`                                                           |
| description | `Issuer-USDCV-Holder`                                                           |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isHolderOf`                                                                    |
| Value       | `USDCV`                                                                         |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| id          | `Investor1-USDCV-Holder`                                                                                   |
| description | `Investor1-USDCV-Holder`                                                                                   |
| Subject     | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `USDCV`                                                                                                    |

| Item        | Value                                                                                                      |
| :---------- | :--------------------------------------------------------------------------------------------------------- |
| holder      | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| id          | `Investor2-USDCV-Holder`                                                                                   |
| description | `Investor2-USDCV-Holder`                                                                                   |
| Subject     | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Property    | `isHolderOf`                                                                                               |
| Value       | `USDCV`                                                                                                    |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-offers-credential-of-token-issuer-and-holder-to-issuer) for details.

### 3.1 Issuer requests token issuance (minting)

| Actors   | Module   | Tab   |
| :------- | :------- | :---- |
| SG Forge | Registry | Mints |

#### EUR10m EURCV issued

| Item       | Value                                                                           |
| :--------- | :------------------------------------------------------------------------------ |
| Instrument | `EURCV-TESTNET`                                                                 |
| Amount     | `10000000`                                                                      |
| Registrar  | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Reference  | `EURCV-TESTNET EUR10m issued Nov-2025`                                          |

#### USD10m USDCV issued

| Item       | Value                                                                           |
| :--------- | :------------------------------------------------------------------------------ |
| Instrument | `USDCV-TESTNET`                                                                 |
| Amount     | `10000000`                                                                      |
| Registrar  | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Reference  | `USDCV-TESTNET USD10m issued Nov-2025`                                          |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-requests-token-issuance-minting) for details.

### 3.2 Registrar accepts and tokens are issued

| Actors   | Module   | Tab   |
| :------- | :------- | :---- |
| SG Forge | Registry | Mints |

Registrar accepts and tokens are issued.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#registrar-accepts-and-tokens-are-issued) for details.

### 3.3 Issuer offers token transfer to Investor1

| Actors   | Module   | Tab      |
| :------- | :------- | :------- |
| SG Forge | Registry | Holdings |

Issuer transfers tokens to Investor1. (3 dots menu on the right of the holding / `Transfer` )

#### EUR8m EURCV placed to Investor1

| Item       | Value                                                                                                      |
| :--------- | :--------------------------------------------------------------------------------------------------------- |
| Send from  | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3`                            |
| Send to    | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Instrument | `EURCV-TESTNET`                                                                                            |
| Amount     | `8000000`                                                                                                  |
| Reference  | `EURCV-TESTNET EUR8m placement to Investor1`                                                               |

#### USD8m USDCV placed to Investor1

| Item       | Value                                                                                                      |
| :--------- | :--------------------------------------------------------------------------------------------------------- |
| Send from  | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3`                            |
| Send to    | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Instrument | `USDCV-TESTNET`                                                                                            |
| Amount     | `8000000`                                                                                                  |
| Reference  | `USDCV-TESTNET USD8m placement to Investor1`                                                               |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-offers-token-transfer-to-investor1) for details.

### 3.4 Investor1 accepts transfer

| Actors    | Module   | Tab       |
| :-------- | :------- | :-------- |
| Investor1 | Registry | Transfers |

Investor1 accepts transfer offer. (click on offer, and then on `Accept`)

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#investor1-accepts-the-transfer-offer-and-tokens-are-transferred) for details.

### 4.1 Investor1 offers token transfer to Investor2

| Actors   | Module   | Tab      |
| :------- | :------- | :------- |
| SG Forge | Registry | Holdings |

Investor1 transfers tokens to Investor2. (3 dots menu on the right of the holding / `Transfer` )

#### EUR3m EURCV transfer from Investor1 to Investor2

| Item       | Value                                                                                                      |
| :--------- | :--------------------------------------------------------------------------------------------------------- |
| Send from  | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Send to    | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Instrument | `EURCV-TESTNET`                                                                                            |
| Amount     | `3000000`                                                                                                  |
| Reference  | `EURCV-TESTNET EUR3m transfer from Investor1 to Investor2`                                                 |

#### USD3m USDCV transfer from Investor1 to Investor2

| Item       | Value                                                                                                      |
| :--------- | :--------------------------------------------------------------------------------------------------------- |
| Send from  | `auth0_007c692dafd3a671ed48e985f245::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Send to    | `auth0_007c692dafef3d5476ff3ddd16e8::1220f36652a7487f93853ac8dcc7ed9e64c32c7caebf8c715e83c8581dba855a37ca` |
| Instrument | `USDCV-TESTNET`                                                                                            |
| Amount     | `3000000`                                                                                                  |
| Reference  | `USDCV-TESTNET USD3m transfer from Investor1 to Investor2`                                                 |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-offers-token-transfer-to-investor1) for details.

### 4.2 Investor2 accepts transfer

| Actors    | Module   | Tab       |
| :-------- | :------- | :-------- |
| Investor2 | Registry | Transfers |

Investor2 accepts transfer offer. (click on offer, and then on `Accept`)

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#investor1-accepts-the-transfer-offer-and-tokens-are-transferred) for details.

## Test 'freeze asset' feature

- SG Forge as Registrar revoked Investor2 "isHolderOf: EURCV" credentials
- Investor2 tries to transfer EURCV => fails
- Investor2 tries to receives EURCV => fails

https://github.com/user-attachments/assets/c01b0bd9-742d-4b13-b77c-09f1c9492704
