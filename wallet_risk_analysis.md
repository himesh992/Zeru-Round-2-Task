
#  Analysis Report: Wallet Risk Scoring

## 1. Data Collection Method
The wallet transaction data was collected via the **[Alchemy API](https://www.alchemy.com/)**, which allows programmatic access to Ethereum blockchain data. For each wallet address, I queried the **transaction count** (both incoming and outgoing) over a specified time period. This method is scalable and can be extended to thousands of wallets with pagination or batching.

## 2. Feature Selection Rationale
After initial data exploration, the following feature was selected for analysis:

- **Transaction Count (`tx_count`)**: This metric reflects wallet activity and potential engagement in financial behavior.

The simplicity and reliability of this feature make it a strong base indicator for risk modeling. Additional features like average transaction size, token transfers, or interaction with known contract addresses can be integrated in future iterations.

## 3. Scoring Method
Each wallet was assigned a **risk score** based on its transaction count. The scoring function was designed to be:
- **Non-linear** to reflect diminishing returns at higher counts.
- **Normalized** so the highest score is capped at 1000.

**Formula used:**
```python
score = min(1000, int(math.log(tx_count + 1) * 100))
```

This approach ensures:
- Low-activity wallets receive proportionally lower scores.
- High-activity wallets quickly approach the maximum score without requiring exact transaction parity.

## 4. Justification of Risk Indicators
The primary risk indicator used here is **wallet activity**:
- **Low Activity** (e.g., 1–2 tx): May indicate dormant, spam, or one-off wallets.
- **Moderate Activity**: Suggests casual or limited use.
- **High Activity** (hundreds+ tx): Typically represents active users, bots, contracts, or higher engagement wallets.

This heuristic assumes that **risk is inversely related to activity**, based on the premise that:
- Dormant wallets may be created for malicious intent (e.g., Sybil attacks, manipulation).
- Active wallets are more likely to be trustworthy or of real users.

> While this is a simple model, it provides a scalable foundation. Future improvements may include additional blockchain metrics (e.g., token holdings, contract interactions, DeFi usage, etc.) and integration with known blacklists or reputation services.
