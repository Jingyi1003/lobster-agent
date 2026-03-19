# 🦞 LobsterAgent

LobsterAgent is a lifestyle decision agent that helps users choose the best food ordering strategy under real-world constraints.

Instead of simply recommending a restaurant, it models food ordering as a **multi-constraint decision problem** involving price, time, distance, coupon uncertainty, user preference, and meal composition.

---

## 🎯 Motivation

Food ordering in real life is not trivial.

Users need to consider:
- Dynamic coupons (e.g., inflation coupons)
- Pickup vs delivery trade-offs
- Budget limits
- Repeated meals over time
- Taste preferences

This project simulates how humans make daily food decisions and builds an agent to automate this process.

---

## ⚙️ Core Features

### 🧠 Multi-factor Decision Making
- Price (after coupons)
- Rating (quality constraint ≥ 4.5)
- Delivery time
- Distance

---

### 📍 Pickup vs Delivery Decision

- If distance ≤ 200m:
  - Choose pickup if it saves more than 2 RMB
- Otherwise:
  - Choose delivery

---

### 💰 Coupon & Pricing System

- Monthly limited coupon packs (choose one):
  - ¥0.99 → 2 coupons
  - ¥6 → 8 coupons
  - ¥12 → 15 coupons
- Each coupon has uncertain value:
  - 5 → 6 / 7 / 9 RMB (inflation)
- Coupons for pickup and delivery are **not interchangeable**
- Agent dynamically decides whether to **use or save coupons**

---

### 🔁 Diversity Constraint

- Main meals are not repeated within 3 days
- Improves variety and user experience

---

### 🧋 Meal Composition

Each recommendation includes:
- 1 main dish
- 1 drink (recommended)
- Optional dessert (within budget)

---

### 🌶️ Context-aware Pairing

- Spicy food → recommend iced drinks
- Enhances dining experience

---

### 🧠 User Feedback Learning

| Score | Behavior |
|------|--------|
| 3 | Prefer again (can repeat soon) |
| 2 | Avoid repeating within 3 days |
| 1 | Permanently removed (blacklist) |

---

### 🔄 Uncertainty Handling

- Coupons may change or fail
- Agent dynamically recalculates decisions (fallback mechanism)

---

## 🔄 Decision Pipeline
```text
[Input] Raw Store Data
    ↓
[Filter] Rating ≥ 4.5
    ↓
[Pricing] Apply coupon inflation
    ↓
[Decision] Pickup vs Delivery
    ↓
[Constraint] 3-day diversity check
    ↓
[Ranking] Score optimization
    ↓
[Composition] Add drink & dessert
    ↓
[Output] Final Recommendation
```
---

## 🧪 Demo Code (Simplified)

```python
stores = [
    {"name": "外婆家", "price": 27, "rating": 4.8, "time": 15, "distance": 150},
    {"name": "和合谷", "price": 24, "rating": 4.8, "time": 31, "distance": 300},
    {"name": "西少爷", "price": 24, "rating": 4.6, "time": 23, "distance": 150},
]

def choose_store(stores):
    best = None
    best_score = float("inf")

    for s in stores:
        if s["rating"] < 4.5:
            continue

        score = s["price"] + s["time"] * 0.1

        if s["distance"] <= 200:
            score -= 2

        if score < best_score:
            best_score = score
            best = s

    return best

result = choose_store(stores)
print("Today's Recommendation:", result["name"])
```
---
## 📊 Example Output

```text
[LobsterAgent Decision Log]

Evaluating candidates...
✔ 外婆家 → rating 4.8, time 15 min, distance 150m
✔ 和合谷 → rating 4.8, time 31 min
✔ 西少爷 → rating 4.6

Applying constraints...
✔ Rating ≥ 4.5
✔ Not ordered in last 3 days

Applying pricing model...
✔ Coupon applied
✔ Pickup advantage considered

Final decision:

Main Dish: 外婆家
Price: ¥27
Method: Delivery

Drink: Iced Lemon Tea
Dessert: Optional
```

Reason:
- Optimal trade-off between price and time
- High rating
- Satisfies diversity constraint
---
## 💡 Key Insight

LobsterAgent models food ordering as:

> A multi-objective decision problem under uncertainty

It balances:
- Cost efficiency  
- Time efficiency  
- Distance constraints  
- User behavior  
- Experience optimization  