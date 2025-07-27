Wallet Risk Score Analysis

 1. Overview of the Dataset

The dataset contains transaction counts (tx_count) and corresponding risk scores (score) for a number of Ethereum wallet addresses. Each row represents a unique wallet.

Metric

Value

Total Wallets

100+

Max Transactions

539

Max Score

1000

Min Transactions

1

Min Score

0

2. Observations

Highly Active Wallets:

Wallets with tx_count > 400 (e.g., 0x9647..., 0xf340..., 0x70d8...) have scores between 780–821. This likely places them in a "high-risk" or "high-activity" zone.

These might represent bots, institutional wallets, or mixers.

Inactive/Low Activity Wallets:

Wallets with only 1 or 2 transactions mostly have scores around 0–59, possibly indicating low risk or untested behavior.

Some wallets with tx_count = 1 have a score = 0—they might be abandoned or newly created with no follow-up activity.

Score Progression:

The score appears to increase non-linearly with transaction count. For example:

tx_count = 1 → score = 0

tx_count = 3 → score = 101

tx_count = 28 → score = 392

tx_count = 433 → score = 789

tx_count = 539 → score = 821

Suggests the score algorithm rewards mid-to-high activity more than low activity.

3. Risk Buckets (Based on Score)

Score Range

Risk Level

Characteristics

0–100

Low

New or dormant wallets

101–300

Moderate

Occasional use

301–600

Medium

Consistent activity, possible DApp users

601–800

High

Power users or repeat patterns

800–1000

Critical

Likely bots, whales, or automated systems

