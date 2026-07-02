# Trading212TickersOdd1Out
# Trading212 ⇄ Yahoo Finance Mapping Collection

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)

Trading212 is a popular commission free stock trading app in the UK and Europe,(If you want to have a trading 212 account,here is referral link, whick rewards free stocks for now (06/26): https://www.trading212.com/invite/GISi2gr9)
Trading212 has a different ticker system as Yahoo Finance.
This project collects and maintains **non‑standard mappings** between Trading212 stock tickers and Yahoo Finance tickers. It helps developers using the Trading212 API to quickly find the correct Yahoo symbol, avoiding data fetch failures caused by inconsistent ticker formats.

## 📌 Background

Most Trading212 tickers (e.g. `LLOYl_EQ`) can be converted to Yahoo Finance symbols (e.g. `LLOY.L`) using a set of predictable rules. However, a significant number of stocks have exceptions due to company renames, SPAC mergers, exchange changes, special suffixes, or ADR simplifications. This project centralises those exceptions and provides a community‑maintained reference.

## 🌍 Standard Mapping Rules

The majority of Trading212 tickers follow these conversion patterns.

### 🇬🇧 UK Stocks (London Stock Exchange)
| Trading212 Format | Yahoo Format | Example |
|-------------------|--------------|---------|
| `xxxl_EQ` or `xxx1_EQ` | `xxx.L` | `LLOYl_EQ` → `LLOY.L`<br>`SHEL1_EQ` → `SHEL.L` |

### 🇺🇸 US Stocks (NYSE / NASDAQ)
| Trading212 Format | Yahoo Format | Example |
|-------------------|--------------|---------|
| `xxx_US_EQ` | `xxx` | `AAPL_US_EQ` → `AAPL`<br>`NVDA_US_EQ` → `NVDA` |
| Note: underscores `_` sometimes become hyphens `-` | | `BRK_B_US_EQ` → `BRK-B` |

### 🇪🇺 European Stocks (Multiple Exchanges)
| Exchange | Trading212 Suffix | Yahoo Suffix | Example |
|----------|-------------------|--------------|---------|
| Paris (Euronext Paris) | `p_EQ` | `.PA` | `AIRp_EQ` → `AIR.PA` |
| Germany (Xetra) | `d_EQ` | `.DE` | `SAPd_EQ` → `SAP.DE` |
| Amsterdam | `a_EQ` | `.AS` | `AKZAa_EQ` → `AKZA.AS` |
| Switzerland | `s_EQ` | `.SW` | `ZURNs_EQ` → `ZURN.SW` |
| Madrid | `e_EQ` | `.MC` | `TEFe_EQ` → `TEF.MC` |

> **Note**: These rules apply to most stocks but are not exhaustive. Always refer to the actual mapping file.

## 🧩 Non‑Standard Mappings (Core of This Project)

The following situations cause mappings to deviate from the standard rules:
- Company rebranding (e.g. `FB` → `META`)
- SPAC mergers (e.g. `VACQ` → `RKLB`)
- Ticker changes (e.g. `RBS` → `NWG`)
- Unusual suffixes (e.g. `.MU`, `.F`)
- ADR code simplifications (e.g. `JBSAY` → `JBS`)

### 📄 Current Collection of Non‑Standard Mappings

| Trading212 Ticker | Yahoo Ticker | Reason |
|-------------------|--------------|--------|
| `LSEl_EQ` | `LSEG.L` | Ticker change (LSE → LSEG) |
| `SLl_EQ` | `ABDN.L` | Ticker change (SL → ABDN) |
| `PHNXl_EQ` | `SDLF.L` | Ticker change (PHNX → SDLF) |
| `RBl_EQ` | `RKT.L` | Ticker change (RB → RKT) |
| `RBSl_EQ` | `NWG.L` | Ticker change (RBS → NWG) |
| `GVCl_EQ` | `ENT.L` | Ticker change (GVC → ENT) |
| `BTl_EQ` | `BT-A.L` | Special suffix (BT → BT-A) |
| `BDEVl_EQ` | `BTRW.L` | Ticker change (BDEV → BTRW) |
| `ICPl_EQ` | `ICG.L` | Ticker change (ICP → ICG) |
| `FB_US_EQ` | `META` | Company rename (Facebook → Meta) |
| `SZZL_US_EQ` | `CRML` | Ticker change (SZZL → CRML) |
| `VACQ_US_EQ` | `RKLB` | SPAC merger (VACQ → RKLB) |
| `OAC_US_EQ` | `HIMS` | SPAC merger (OAC → HIMS) |
| `IPOE_US_EQ` | `SOFI` | SPAC merger (IPOE → SOFI) |
| `DMYI_US_EQ` | `IONQ` | SPAC merger (DMYI → IONQ) |
| `IPXX_US_EQ` | `USAR` | SPAC merger (IPXX → USAR) |
| `SV_US_EQ` | `SMR` | Ticker change (SV → SMR) |
| `NPA_US_EQ` | `ASTS` | SPAC merger (NPA → ASTS) |
| `UTX_US_EQ` | `RTX` | Corporate split/merger (UTX → RTX) |
| `SNII_US_EQ` | `RGTI` | Ticker change (SNII → RGTI) |
| `BSGA_US_EQ` | `BTDR` | SPAC merger (BSGA → BTDR) |
| `GNPK_US_EQ` | `RDW` | SPAC merger (GNPK → RDW) |
| `JBSAY_US_EQ` | `JBS` | ADR code simplification (JBSAY → JBS) |
| `FPp_EQ` | `TTE.PA` | Company rename (FP → TTE) |
| `DAId_EQ` | `MBG.DE` | Company rename (DAI → MBG) |
| `NTOd_EQ` | `NTO.MU` | Exchange suffix anomaly (expected .DE, got .MU) |
| `2DGd_EQ` | `2DG.F` | Exchange suffix anomaly (expected .DE, got .F) |
| `FLUIes_EQ` | `FDR.MC` | Ticker change (FLUI → FDR) |

> The full list is maintained in [`odd_mappings.csv`](./odd_mappings.csv).

## 🤝 How to Contribute

We welcome contributions of new mappings or corrections to existing ones. You can participate by:

1. **Fork this repository**
2. **Add or update `odd_mappings.csv`**: Please keep the format `original_ticker,yahoo_ticker,reason` (three columns).
3. **Submit a Pull Request**: Briefly explain the basis for your mapping (e.g., official company announcement, exchange notice, etc.).

### Contribution Guidelines
- Ensure the mapping you add is genuinely non‑standard (cannot be derived by standard rules).
- If you find a mapping that is outdated or incorrect, please suggest a fix.
- Provide a source reference if possible (e.g., Trading212 official documentation, Yahoo Finance query results, etc.).

## 📚 Related Resources

- [Trading212 API Documentation](https://docs.trading212.com/api)
- [Yahoo Finance API (yfinance)](https://github.com/ranaroussi/yfinance)
- [Trading212 Community Forum](https://community.trading212.com)

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](./LICENSE) file for details.

---
