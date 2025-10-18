# 2-Player Duel: Pure Mathematical Logic

## Core Mathematical Framework

### **Round Winner Determination**
The player with **higher net winnings** wins each round.

```
Net Winnings = Total Winnings - Total Bet Amount
Round Winner = argmax(Net Winnings)
```

### **Mathematical Formula**
```
For Player i in round r:
Net_i(r) = Σ(j∈WinningItems) (Bet_i(j) × Multiplier_j) - Σ(j∈AllBets) Bet_i(j)

Where:
- Bet_i(j) = Amount player i bet on item j
- Multiplier_j = Payout multiplier for item j
- WinningItems = Items that won the roulette spin
```

## Duel Scoring Mathematics

### **Duel Score Vector**
```
S = [S_A, S_B]
Where S_A = Rounds won by Player A
      S_B = Rounds won by Player B
```

### **Winning Conditions**
```
Duel Winner = {
  Player A, if S_A = 2
  Player B, if S_B = 2  
  Round 3 Winner, if S_A = S_B = 1 after Round 2
}
```

## House Edge Mathematics

### **House Edge Formula**
```
House Edge = Variable, averaging ~10%
Users can have positive EV on some items
```

### **Item Multiplier Calculation**
```
For positive EV items: P_j × Multiplier_j > 1.0
For negative EV items: P_j × Multiplier_j < 1.0
Average across all items: ~0.90 (10% house edge)
```

## Bot vs User EV Mathematics

### **User Expected Value (Variable)**
```
EV_User = Σ(j) Bet_User(j) × (P_j × Multiplier_j - 1)

High probability items: EV_User > 0 (positive)
Low probability items: EV_User < 0 (negative)
Average across all bets: ~-10% (house edge)
```

### **Bot Expected Value (Positive)**
```
EV_Bot = Σ(j) Bet_Bot(j) × (P_j × Multiplier_j - 1) + Bot_Advantage

Bot focuses on positive EV items + strategic advantage
EV_Bot > EV_User (bot outperforms user)
```

## Bot Advantage Mathematics

### **Bot Advantage Sources**
```
Bot_Advantage = Information_Advantage + Strategic_Advantage

Where:
Information_Advantage = Bot knows optimal betting patterns
Strategic_Advantage = Bot can exploit user's suboptimal play
```

### **Mathematical Bot Advantage**
```
Bot_Advantage = α × House_Edge + β × User_Mistakes

Where:
α = Bot's ability to minimize house edge (0.1-0.3)
β = Bot's ability to exploit user errors (0.05-0.15)
```

### **Example Item Math**
```
High Probability Items (User Positive EV):
- 50% probability: 2.2x multiplier → EV = 0.50 × 2.2 - 1 = +0.10 (+10%)
- 40% probability: 2.8x multiplier → EV = 0.40 × 2.8 - 1 = +0.12 (+12%)

Medium Probability Items (Slightly Negative EV):
- 30% probability: 3.2x multiplier → EV = 0.30 × 3.2 - 1 = -0.04 (-4%)
- 25% probability: 3.8x multiplier → EV = 0.25 × 3.8 - 1 = -0.05 (-5%)

Low Probability Items (Higher Negative EV):
- 15% probability: 5.5x multiplier → EV = 0.15 × 5.5 - 1 = -0.175 (-17.5%)
- 10% probability: 7.5x multiplier → EV = 0.10 × 7.5 - 1 = -0.25 (-25%)

Very Low Probability Items (High Negative EV):
- 5% probability: 12x multiplier → EV = 0.05 × 12 - 1 = -0.40 (-40%)
- 2% probability: 25x multiplier → EV = 0.02 × 25 - 1 = -0.50 (-50%)
```

## Bot Strategy Mathematics

### **Bot Optimal Betting**
```
Bot maximizes: E[Net_Bot] = Σ(j) Bet_Bot(j) × (P_j × Multiplier_j - 1) + Bot_Advantage

Subject to:
- Σ(j) Bet_Bot(j) ≤ Bankroll_Bot
- Bet_Bot(j) ≥ 0
```

### **Bot vs User Probability**
```
P(Bot wins round) = P(Net_Bot > Net_User)

Where:
Net_Bot ~ Normal(E[Net_Bot], Var[Net_Bot])
Net_User ~ Normal(E[Net_User], Var[Net_User])
```

## Mathematical Constraints

### **House Edge Constraint**
```
House Profit = Variable, averaging ~10% across all bets
Some items favor users (positive EV)
Some items favor house (negative EV)
```

### **Bot Advantage Constraint**
```
Bot_Advantage ≤ 0.20 × Total_Bet_Bot
(Bot advantage capped at 20% of bot's bets)
```

### **User Protection Constraint**
```
High probability items: EV_User ≥ +0.05 (5% minimum positive)
Overall average: EV_User ≥ -0.15 (15% maximum negative)
```

## Duel Win Probability

### **Bot Win Probability**
```
P(Bot wins duel) = P(Bot wins 2+ rounds out of 3)

Where P(Bot wins round) = P(Net_Bot > Net_User)
```

### **Mathematical Approximation**
```
P(Bot wins round) ≈ 0.65-0.75 (due to bot advantage)
P(Bot wins duel) ≈ 0.70-0.80 (due to 3-round format)
```


## Mathematical Examples

### **Example 1: User vs Bot with Variable EV**
```
User bets: 100 on 50% item (2.2x multiplier) → EV = +10%
Bot bets: 100 on 40% item (2.8x multiplier) → EV = +12%

Roulette Result: Bot's item wins

User Net: 0 - 100 = -100
Bot Net: 280 - 100 + 20 = +200

Bot wins: +200 vs -100
```

### **Example 2: Both Win with Different EVs**
```
User Net: 220 - 100 = +120 (won 50% item)
Bot Net: 280 - 100 + 20 = +200 (won 40% item)

Bot wins: +200 vs +120 (both positive, bot better)
```

### **Example 3: Expected Value Comparison**
```
For User's bet on 50% item (2.2x multiplier):
EV_User = 0.50 × 2.2 - 1 = +0.10 (+10%)

For Bot's bet on 40% item (2.8x multiplier):
EV_Bot = 0.40 × 2.8 - 1 + 0.20 = +0.32 (+32%)

Bot has significantly better EV
```

## Key Mathematical Insights

### **1. House Variable Profit**
```
House Profit = Variable, averaging ~10% across all bets
High probability items: House loses money
Low probability items: House makes money
```

### **2. Bot Advantage**
```
E[Net_Bot] > E[Net_User] due to:
- Better item selection (focuses on positive EV)
- Strategic advantage
- Information advantage
```

### **3. User Opportunity**
```
Users can earn money on high probability items
Users lose money on low probability items
Strategic item selection determines success
```

This mathematical framework provides the pure logic for determining winners, calculating probabilities, and optimizing strategies in the 2-player duel system.
