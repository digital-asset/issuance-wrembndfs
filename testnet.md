# Testnet Issuance - November, 2025 <!-- omit in toc -->

## Table of Contents <!-- omit in toc -->

- [Documentation](#documentation)
- [URLs \& Versions](#urls--versions)
- [PartyIDs](#partyids)
- [Status](#status)
  - [Step 1: Onboarding roles](#step-1-onboarding-roles)
  - [Step 2: Configuring tokens](#step-2-configuring-tokens)
  - [Step 3: Issuing tokens](#step-3-issuing-tokens)
- [Detailed instructions](#detailed-instructions)
  - [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities)
  - [1.2 Provider credential](#12-provider-credential)
  - [1.3 Onboard Provider](#13-onboard-provider)
  - [1.4 Onboarding requirements for registrars and holders](#14-onboarding-requirements-for-registrars-and-holders)
  - [1.5 / 1.6 Registrar credential](#15--16-registrar-credential)
  - [1.10 / 1.11 Registrar onboarding](#110--111-registrar-onboarding)
  - [2.1 Registrar creates Allocation Factory, Transfer Rule and specifies Instrument Configuration](#21-registrar-creates-allocation-factory-transfer-rule-and-specifies-instrument-configuration)
  - [2.2 / 2.3 / 2.4 / 2.5 Registrar offers credential to Issuer and Holders](#22--23--24--25-registrar-offers-credential-to-issuer-and-holders)
  - [3.1 Issuer requests token issuance (minting)](#31-issuer-requests-token-issuance-minting)
  - [3.2 Registrar accepts and tokens are issued](#32-registrar-accepts-and-tokens-are-issued)
  - [3.3 Issuer offers token transfer to Investors](#33-issuer-offers-token-transfer-to-investors)
  - [3.4 Investor accepts transfer](#34-investor-accepts-transfer)

## Documentation

- [Issuing Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/introduction.html)
- [Transfering Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/transfer/index.html)
- [Redeeming Tokenized Instruments](https://docs.digitalasset.com/utilities/testnet/tutorials/redemption/index.html)

## URLs & Versions

| Entity            | Details                                                        | Utility UI version |
| :---------------- | :------------------------------------------------------------- | ------------------ |
| SG Forge (SGF)    | https://utility-socgen.test.broadridge.catalyst.intellecteu.io | 0.10.2 TBC         |
| DRW TBC (DRW)     | xyz                                                            | 0.10.2 TBC         |
| Virtu TBC (Virtu) | xyz                                                            | 0.10.2 TBC         |

## PartyIDs

| Entity   | Party ID                                                                        |
| :------- | :------------------------------------------------------------------------------ |
| SG Forge | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| DRWS     | `TBC`                                                                           |
| Virtu    | `TBC`                                                                           |

## Status

### Step 1: Onboarding roles

| Steps                                                                                                            | DA   | BR      | SGF  | SGPM | DRWS |
| :--------------------------------------------------------------------------------------------------------------- | :--- | :------ | :--- | :--- | :--- |
| [1.1 Credential User Service for all entities](#11-credential-user-service-for-all-entities)                     | -    | ✅       | ✅    | ✅    | ✅    |
| [1.2 Provider credential](#12-provider-credential)                                                               | ✅    | ✅ by DA | -    | -    | -    |
| [1.3 Onboard Provider](#13-onboard-provider)                                                                     | -    | ✅ by DA | -    | -    | -    |
| [1.4 Onboarding requirements for registrars and holders](#14-onboarding-requirements-for-registrars-and-holders) | -    | ✅ by DA | -    | -    | -    |
| [1.5 / 1.6 Registrar credential](#15--16-registrar-credential)                                                   | -    | ✅ by DA | ✅    | -    | -    |
| [1.10 / 1.11 Registrar onboarding](#110--111-registrar-onboarding)                                               | -    | ✅       | ✅    | -    | -    |

### Step 2: Configuring tokens

| Steps                                                                                                                                                                                           | DA   | BR   | SGF  | SGPM | DRWS |
| :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :--- | :--- | :--- | :--- | :--- |
| [2.1 Registrar creates Allocation Factory, Transfer Rule and specifies Instrument Configuration](#21-registrar-creates-allocation-factory-transfer-rule-and-specifies-instrument-configuration) | -    | -    | ✅    | -    | -    |
| [2.2 / 2.3 / 2.4 / 2.5 Registrar offers credential to Issuer and Holders](#22--23--24--25-registrar-offers-credential-to-issuer-and-holders)                                                    | -    | -    | ✅    | ✅    | ✅    |

### Step 3: Issuing tokens

| Steps                                                                                          | DA   | BR   | SGF  | SGPM | DRWS |
| :--------------------------------------------------------------------------------------------- | :--- | :--- | :--- | :--- | :--- |
| [3.1 Issuer requests token issuance (minting)](#31-issuer-requests-token-issuance-minting)     | -    | -    | -    | ✅    | -    |
| [3.2 Registrar accepts and tokens are issued](#32-registrar-accepts-and-tokens-are-issued)     | -    | -    | ✅    | -    | -    |
| [3.3 Issuer offers token transfer to Investors](#33-issuer-offers-token-transfer-to-investors) | -    | -    | -    | ✅    | -    |
| [3.4 Investor accepts transfer](#34-investor-accepts-transfer)                                 | -    | -    | -    | -    | ✅    |

## Detailed instructions

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
| holder      | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259` |
| id          | `Broadridge provider`                                                                       |
| description | `Broadridge provider`                                                                       |
| Subject     | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259` |
| Property    | `hasRegistryRole`                                                                           |
| Value       | `Provider`                                                                                  |

| Item        | Value                                                                                                   |
| :---------- | :------------------------------------------------------------------------------------------------------ |
| beneficiary | `DigitalAsset-UtilityFeeReceiver::12202679f2bbe57d8cba9ef3cee847ac8239df0877105ab1f01a77d47477fdce1204` |
| weight      | 0.20                                                                                                    |

| Actors | Module   | Tab                   |
| :----- | :------- | :-------------------- |
| DA, BR | Settings | Commercial Agreements |

DA offers Commercial Agreement, and BR accepts it:

| Item                   | Value                                                                                                   |
| :--------------------- | :------------------------------------------------------------------------------------------------------ |
| user                   | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259`             |
| fee receiver           | `DigitalAsset-UtilityFeeReceiver::12202679f2bbe57d8cba9ef3cee847ac8239df0877105ab1f01a77d47477fdce1204` |
| credential billing fee | 1.75 USD                                                                                                |
| base fee per day       | 0.00 USD                                                                                                |
| billing period         | 10 min                                                                                                  |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#provider-credential) for details.

### 1.3 Onboard Provider

| Actors | Module   | Tab        |
| :----- | :------- | :--------- |
| DA, BR | Registry | Onboarding |

BR clicks on `Requests Provider Service`, and DA accepts.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#onboard-provider) for details.

### 1.4 Onboarding requirements for registrars and holders

| Actors | Module   | Tab           |
| :----- | :------- | :------------ |
| BR     | Registry | Configuration |

BR creates a Provider Configuration.

Required credentials for Holders

| Item              | Value                                                                                       |
| :---------------- | :------------------------------------------------------------------------------------------ |
| Credential Issuer | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259` |
| Property          | `hasRegistryRole`                                                                           |
| Value             | `Holder`                                                                                    |

Required credentials for Registrars

| Item              | Value                                                                                       |
| :---------------- | :------------------------------------------------------------------------------------------ |
| Credential Issuer | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259` |
| Property          | `hasRegistryRole`                                                                           |
| Value             | `Registrar`                                                                                 |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#onboarding-requirements-for-registrars-and-holders) for details.

### 1.5 / 1.6 Registrar credential

| Actors  | Module     | Tab                 |
| :------ | :--------- | :------------------ |
| BR, SGF | Credential | Credentials, Offers |

BR offers a free Registrar credential (Credentials tab), and SGF accepts it (Offers tab).

| Item        | Value                                                                           |
| :---------- | :------------------------------------------------------------------------------ |
| holder      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `SG Forge registrar`                                                            |
| description | `SG Forge registrar`                                                            |
| Subject     | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `hasRegistryRole`                                                               |
| Value       | `Registrar`                                                                     |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#provider-offers-registrar-credential)for details.

### 1.10 / 1.11 Registrar onboarding

| Actors  | Module   | Tab        |
| :------ | :------- | :--------- |
| SGF, BR | Registry | Onboarding |

SGF clicks on `Request Registrar Service`, and BR accepts.

| Item     | Value                                                                                       |
| :------- | :------------------------------------------------------------------------------------------ |
| Provider | `broadridge-provider::1220992258bad53ba6cb1aa634bb912d457f3e0382892ced2d00b4cac654e6e52259` |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/1-onboarding.html#registrar-requests-onboarding-as-a-registrar-in-the-registry) for details.

### 2.1 Registrar creates Allocation Factory, Transfer Rule and specifies Instrument Configuration

| Actors | Module   | Tab           |
| :----- | :------- | :------------ |
| SGF    | Registry | Configuration |

SGF clicks on `Create Allocation Factory` and `Create Transfer Rule`.

Both boxes should turn from blue to grey.

![Allocation Factory Transfer Rule](images/AllocationFactory-TransferRule.png)

SGF creates Instrument Configuration:

| Item                        | Value                                                                           |
| :-------------------------- | :------------------------------------------------------------------------------ |
| Instrument ID               | `SGNOTES-[CUSIP]-TESTNET`                                                       |
| Identifiers                 |                                                                                 |
| Source                      | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Id                          | `[CUSIP]`                                                                       |
| Scheme                      | CUSIP                                                                           |
| Requirement for Mint Issuer |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isIssuerOf`                                                                    |
| Value                       | `SGNOTES`                                                                       |
| Requirement for Holders     |                                                                                 |
| Credential Issuer           | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property                    | `isHolderOf`                                                                    |
| Value                       | `SGNOTES`                                                                       |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-specifying-the-requirement-of-the-bond-token) for details.

### 2.2 / 2.3 / 2.4 / 2.5 Registrar offers credential to Issuer and Holders

| Actors          | Module     | Tab                 |
| :-------------- | :--------- | :------------------ |
| SGF, SGPM, DRWS | Credential | Credentials, Offers |

SGF issues free credentials (Credentials tab), and SGPM / DRWS accept them (Offers tab).

SG Paris Issuer of SGNOTES credential:

| Item        | Value                                                                        |
| :---------- | :--------------------------------------------------------------------------- |
| holder      | `sgpm::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `SGPM-SGNOTES-Issuer`                                                        |
| description | `SGPM-SGNOTES-Issuer`                                                        |
| Subject     | `sgpm::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isIssuerOf`                                                                 |
| Value       | `SGNOTES`                                                                    |

SG Paris Holder of SGNOTES credential:

| Item        | Value                                                                        |
| :---------- | :--------------------------------------------------------------------------- |
| holder      | `sgpm::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| id          | `SGPM-SGNOTES-Holder`                                                        |
| description | `SGPM-SGNOTES-Holder`                                                        |
| Subject     | `sgpm::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Property    | `isHolderOf`                                                                 |
| Value       | `SGNOTES`                                                                    |

DRWS Holder of SGNOTES credential

| Item        | Value                                                                                     |
| :---------- | :---------------------------------------------------------------------------------------- |
| holder      | `Cumberland-DRWS-1::12209d887b76480848434826589f69cb2ca46a670bc948fbc75bccfe933b78f2dd94` |
| id          | `DRWS-SGNOTES-Holder`                                                                     |
| description | `DRWS-SGNOTES-Holder`                                                                     |
| Subject     | `Cumberland-DRWS-1::12209d887b76480848434826589f69cb2ca46a670bc948fbc75bccfe933b78f2dd94` |
| Property    | `isHolderOf`                                                                              |
| Value       | `SGNOTES`                                                                                 |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/2-credentials.html#registrar-offers-credential-of-token-issuer-and-holder-to-issuer) for details.

### 3.1 Issuer requests token issuance (minting)

| Actors | Module   | Tab   |
| :----- | :------- | :---- |
| SGPM   | Registry | Mints |

| Item       | Value                                                                           |
| :--------- | :------------------------------------------------------------------------------ |
| Instrument | `SGNOTES-[CUSIP]-TESTNET`                                                       |
| Amount     | `1000000`                                                                       |
| Registrar  | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3` |
| Reference  | `SGNOTES-[CUSIP]-TESTNET $1m issued Oct-2025`                                   |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-requests-token-issuance-minting) for details.

### 3.2 Registrar accepts and tokens are issued

| Actors | Module   | Tab   |
| :----- | :------- | :---- |
| SGF    | Registry | Mints |

SGF accepts and tokens are issued.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#registrar-accepts-and-tokens-are-issued) for details.

### 3.3 Issuer offers token transfer to Investors

| Actors | Module   | Tab      |
| :----- | :------- | :------- |
| SGPM   | Registry | Holdings |

SGPM transfers tokens to DRWS

| Item       | Value                                                                                     |
| :--------- | :---------------------------------------------------------------------------------------- |
| Receiver   | `Cumberland-DRWS-1::12209d887b76480848434826589f69cb2ca46a670bc948fbc75bccfe933b78f2dd94` |
| Instrument | `SGNOTES-[CUSIP]-TESTNET`                                                                 |
| Amount     | `1000000`                                                                                 |
| Registar   | `sgforge::12206c7de045405eb47f7ecfb1fa82665672664e4b9ab350b7064ef7bceb8bc8cbe3`           |
| Reference  | `SGNOTES-[CUSIP]-TESTNET $1m placement to DRWS`                                           |

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#issuer-offers-token-transfer-to-investor1) for details.

### 3.4 Investor accepts transfer

| Actors | Module   | Tab       |
| :----- | :------- | :-------- |
| DRWS   | Registry | Transfers |

DRWS accepts transfer offer.

See [tutorial](https://docs.digitalasset.com/utilities/testnet/tutorials/issuance/3-issuance.html#investor1-accepts-the-transfer-offer-and-tokens-are-transferred) for details.
