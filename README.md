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
