# iGaming Domain Interview Questions

## What is iGaming

<details>
<summary><b>What do you know about iGaming?</b></summary>

iGaming is the online gambling industry including: casinos, slots, live casino, sports betting, and poker platforms. They operate in real-time under strict regulations.

From frontend perspective: high performance requirements, real-time data handling, mobile-first UX, security focus, and responsible gambling features.

**Main products:**
- **Online Casino**: Slots, RNG games (roulette, blackjack), jackpot mechanics
- **Live Casino**: Real dealers, video streaming, minimal latency
- **Sportsbook**: Live betting, real-time odds updates, cashout features
</details>

## Technical Challenges

<details>
<summary><b>What are the key technical challenges in iGaming frontend?</b></summary>

**Real-time requirements:**
- WebSockets / Server-Sent Events for live data
- Frequent UI updates (odds, game state)
- Interface must handle real-time data and state updates correctly

**High load:**
- Peak events (matches, tournaments)
- Thousands of concurrent users
- Performance and render optimization critical for live odds updates

**Mobile-first:**
- Majority of users are mobile
- Touch UX optimization
- Works on low-end devices
</details>

## Regulations & Compliance

<details>
<summary><b>What should you know about iGaming regulations?</b></summary>

**Licenses:**
- MGA (Malta)
- UKGC (UK Gambling Commission)
- Curacao

Platforms operate under strict regulation and licensing, which affects UX, validation, and user flows.

**Responsible Gambling (important to mention):**
- Deposit limits
- Self-exclusion options
- Reality checks (time/spending alerts)

**KYC / AML:**
- Identity verification
- Regional restrictions
- Age verification
</details>

## Frontend Security in iGaming

<details>
<summary><b>What security considerations are important for iGaming frontend?</b></summary>

Frontend doesn't store money, but:
- **XSS is critical** - can steal sessions, tokens
- **Token handling** - secure storage, refresh flows
- **Session management** - timeouts, concurrent sessions
- **Anti-fraud UX** - suspicious activity detection

Key phrase: "On frontend, minimizing attack surface is crucial, especially considering financial operations."
</details>

## UX Specifics

<details>
<summary><b>What UX patterns are specific to iGaming?</b></summary>

- Minimal time to first action (bet/spin)
- Animations for engagement (but not at performance cost)
- Clear feedback for bets and results
- Errors must be obvious and immediate
- Semantic markup, asset optimization, fast/stable UI under high load
</details>

## Interview Tips

<details>
<summary><b>What NOT to say in iGaming interviews?</b></summary>

Avoid:
- "I know nothing about iGaming"
- "It's just websites with games"
- "Frontend isn't that important here"

Instead, show you understand: industry specifics, technical challenges, regulatory environment, and how frontend skills apply.
</details>
