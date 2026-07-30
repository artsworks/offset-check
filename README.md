# Mortgage Offset Health Check Tool

A lightweight, single-file HTML utility designed to audit monthly Australian home loan interest charges and detect unlinked or non-functioning mortgage offset accounts, aligned with **ASIC 26-173MR** regulatory findings.

---

## Overview

Following ASIC's Report 837, which revealed over **$55 million** in customer compensation due to bank failures in linking offset accounts, this tool provides home owners with a fast, zero-install method to verify if their offset balance is actively reducing home loan interest.

---

## Key Features

* **Zero Installation**: Single static HTML/JavaScript file runnable in any web browser on desktop or mobile.
* **100% Privacy-Preserving**: Runs locally in the browser with no external network calls or data storage.
* **Single-Month Focus**: Requires only 5 input values from a monthly bank statement or mobile banking app.
* **Automated Status Signal**: Instantly categorises offset account health into clear visual badges based on mathematical bounds.

---

## Quick Start

1. Download or save `offset_checker.html`.
2. Double-click the file to open it in any web browser.
3. Input your home loan figures for the target month:
   * **Average Loan Balance**
   * **Average Offset Balance**
   * **Annual Interest Rate (% p.a.)**
   * **Statement Cycle Days** (28, 30, or 31)
   * **Actual Interest Charged** (from banking app)

---

## Status Classification Matrix

| Status | Condition | Meaning |
|---|---|---|
| **🟢 SAFE: Offset Applied** | $\|I_{\text{actual}} - I_{\text{expected}}\| \le \text{Tolerance}$ | Offset account is properly linked and actively saving interest. |
| **🔴 ALERT: Offset Failed** | $\|I_{\text{actual}} - I_{\text{full}}\| \le \text{Tolerance}$ | Interest charged reflects full loan balance without offset deduction. Contact bank immediately. |
| **🟡 UNCERTAIN / PARTIAL** | $I_{\text{expected}} < I_{\text{actual}} < I_{\text{full}}$ | Interest charged differs from static balance estimates (often due to daily balance fluctuations). |

---

## Calculation Formula

The tool calculates expected monthly interest using the standard Australian daily accrual convention:

$$I_{\text{expected}} = \max(0, \text{Loan Balance} - \text{Offset Balance}) \times \left(\frac{\text{Interest Rate}}{365}\right) \times \text{Cycle Days}$$

$$I_{\text{full}} = \text{Loan Balance} \times \left(\frac{\text{Interest Rate}}{365}\right) \times \text{Cycle Days}$$
