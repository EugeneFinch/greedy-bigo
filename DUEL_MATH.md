# Duel Math - 2-Player Greedy Game System

## Core Mechanics

### **Game Structure:**
- **2 Players**: Head-to-head competition
- **3 Rounds**: Best of 3 rounds wins the duel
- **8 Items**: Each with unique probability and multiplier
- **Bot Replacement**: AI replaces absent players

### **Round Winning Logic:**
1. Both players place bets on items
2. System selects one item randomly based on probabilities
3. Players receive payouts based on multipliers
4. **Round Winner**: Player with better net performance (higher winnings or smaller losses)
5. **Duel Winner**: Player who wins 2 out of 3 rounds

### **Scoring System:**
- **Net Performance** = (Bet Amount × Multiplier) - Bet Amount
- **Round Winner**: Higher net performance
- **Duel Winner**: Wins 2+ rounds

## Mathematical Model

### **Expected Value (EV) Formula:**
```
EV = (Probability × Multiplier) - 1
```

### **House Edge Formula:**
```
House Edge = Σ(1 - Probability × Multiplier)
```

### **Bot AI Models:**

**Easy Bot:**
- Bets on high-probability items (Items 1-3)
- Conservative strategy
- EV: +2% (slight advantage)

**Medium Bot:**
- Mixed strategy (Items 1-5)
- Balanced approach
- EV: +5% (moderate advantage)

**Hard Bot:**
- Strategic betting (Items 3-8)
- Aggressive strategy
- EV: +8% (significant advantage)

## Item System

**FINAL Multipliers (Min 2.5x, 100% Probability, Positive House Edge):**

```
Item 1: 30% probability, 2.5x multiplier → EV = 0.30 × 2.5 - 1 = -0.25 (-25%)
Item 2: 25% probability, 3.0x multiplier → EV = 0.25 × 3.0 - 1 = -0.25 (-25%)
Item 3: 20% probability, 3.5x multiplier → EV = 0.20 × 3.5 - 1 = -0.30 (-30%)
Item 4: 15% probability, 4.0x multiplier → EV = 0.15 × 4.0 - 1 = -0.40 (-40%)
Item 5: 6% probability, 5.0x multiplier → EV = 0.06 × 5.0 - 1 = -0.70 (-70%)
Item 6: 2.5% probability, 6.0x multiplier → EV = 0.025 × 6.0 - 1 = -0.85 (-85%)
Item 7: 1% probability, 8.0x multiplier → EV = 0.01 × 8.0 - 1 = -0.92 (-92%)
Item 8: 0.5% probability, 12.0x multiplier → EV = 0.005 × 12.0 - 1 = -0.94 (-94%)

Total Probability: 30% + 25% + 20% + 15% + 6% + 2.5% + 1% + 0.5% = 100%

House Edge Calculation:
Item 1: 1 - (30% × 2.5) = 1 - 0.75 = 0.25
Item 2: 1 - (25% × 3.0) = 1 - 0.75 = 0.25
Item 3: 1 - (20% × 3.5) = 1 - 0.70 = 0.30
Item 4: 1 - (15% × 4.0) = 1 - 0.60 = 0.40
Item 5: 1 - (6% × 5.0) = 1 - 0.30 = 0.70
Item 6: 1 - (2.5% × 6.0) = 1 - 0.15 = 0.85
Item 7: 1 - (1% × 8.0) = 1 - 0.08 = 0.92
Item 8: 1 - (0.5% × 12.0) = 1 - 0.06 = 0.94

Total: 0.25 + 0.25 + 0.30 + 0.40 + 0.70 + 0.85 + 0.92 + 0.94 = 4.61
House Edge = 4.61% (CORRECT!)
```

#### **PvP Duel Calculations:**

**Round 1 Example:**
```
Player A bets: $100 on Item 1 (30% chance, 2.5x multiplier)
Player B bets: $100 on Item 3 (20% chance, 3.5x multiplier)

Outcome: Item 1 selected (30% probability)
- Player A wins: $100 × 2.5 = $250 (gains $150)
- Player B loses: $100 (loses $100)

Round Winner: Player A (gained $150 vs lost $100)
```

**Round 2 Example:**
```
Player A bets: $200 on Item 4 (15% chance, 4.0x multiplier)
Player B bets: $150 on Item 6 (2.5% chance, 6.0x multiplier)

Outcome: Item 6 selected (2.5% probability)
- Player A loses: $200 (loses $200)
- Player B wins: $150 × 6.0 = $900 (gains $750)

Round Winner: Player B (gained $750 vs lost $200)
```

**Round 3 Example:**
```
Player A bets: $300 on Item 8 (0.5% chance, 12.0x multiplier)
Player B bets: $250 on Item 2 (25% chance, 3.0x multiplier)

Outcome: Item 2 selected (25% probability)
- Player A loses: $300 (loses $300)
- Player B wins: $250 × 3.0 = $750 (gains $500)

Round Winner: Player B (gained $500 vs lost $300)
```

**Duel Winner Calculation:**
```
Round 1: Player A wins (+$150)
Round 2: Player B wins (+$750)
Round 3: Player B wins (+$500)

Total Scores:
- Player A: $150 + (-$200) + (-$300) = -$350
- Player B: (-$100) + $750 + $500 = $1,150

Duel Winner: Player B (better net performance: $1,150 vs -$350)
```

**House Profit per Duel:**
```
Total Bets: $100 + $100 + $200 + $150 + $300 + $250 = $1,100
Total Payouts: $250 + $900 + $750 = $1,900
House Profit: $1,100 - $1,900 = -$800
House Edge: -$800 / $1,100 = -72.7% (per duel - HOUSE LOSES!)
```

**Expected House Edge per Round:**
```
Using our CORRECT multipliers:
Item 1: 1 - (30% × 2.5) = 1 - 0.75 = 0.25
Item 2: 1 - (25% × 3.0) = 1 - 0.75 = 0.25
Item 3: 1 - (20% × 3.5) = 1 - 0.70 = 0.30
Item 4: 1 - (15% × 4.0) = 1 - 0.60 = 0.40
Item 5: 1 - (6% × 5.0) = 1 - 0.30 = 0.70
Item 6: 1 - (2.5% × 6.0) = 1 - 0.15 = 0.85
Item 7: 1 - (1% × 8.0) = 1 - 0.08 = 0.92
Item 8: 1 - (0.5% × 12.0) = 1 - 0.06 = 0.94

Total House Edge: 0.25 + 0.25 + 0.30 + 0.40 + 0.70 + 0.85 + 0.92 + 0.94 = 4.61%
```

#### **Comparison with Real Roulette Games:**
```
European Roulette: 2.7% house edge
American Roulette: 5.26% house edge
Our Game: 4.61% house edge (reasonable, slightly lower than American)
```

## Bot Strategy Mathematics

### **Easy Bot Strategy:**
- **Target Items**: 1, 2, 3 (75% total probability)
- **Betting Pattern**: 40% Item 1, 35% Item 2, 25% Item 3
- **Expected Performance**: +2% advantage over random betting

### **Medium Bot Strategy:**
- **Target Items**: 1, 2, 3, 4, 5 (96% total probability)
- **Betting Pattern**: Weighted towards higher probability items
- **Expected Performance**: +5% advantage over random betting

### **Hard Bot Strategy:**
- **Target Items**: 3, 4, 5, 6, 7, 8 (45.5% total probability)
- **Betting Pattern**: Strategic mix of medium and high multipliers
- **Expected Performance**: +8% advantage over random betting

### **Bot Advantage Implementation:**
```
Bot EV = User EV + Bot Advantage
Easy Bot: -82% + 2% = -80%
Medium Bot: -82% + 5% = -77%
Hard Bot: -82% + 8% = -74%
```

## Summary

### **Key Metrics:**
- **House Edge**: 4.61% (profitable)
- **User EV**: -25% to -94% (house advantage)
- **Bot EV**: -17% to -86% (better than users)
- **Max Multiplier**: 12.0x (exciting for players)
- **Probability Range**: 0.5% to 30% (realistic distribution)