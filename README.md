# Thracian Treasure Slot Simulation

Slot machine game simulation.

## Building & Running

javac Main.java

java Main -help

java Main -g100m -p10k

java Main -verify

## Source Code Formatting

astyle *.java --indent=force-tab --style=java / -A2 --recursive

## Volatility Calculation

Volatility in slot machine models is primarily calculated as the **Standard Deviation ($\\sigma$)** of the game's payout distribution. While mathematical "Volatility" is a raw statistical value, the 1-to-5 star rating used by developers (like Pragmatic Play) is a **normalized score** that weights several factors including win frequency and maximum win potential. \[1, 2\]

### **1\. Calculate the Base Mathematical Volatility**

To find the core volatility, you must calculate the standard deviation of all possible outcomes. If you are simulating the game, run at least **1 million spins** to get a stable result. \[2\]

$$\\sigma \= \\sqrt{\\sum P\_i \\cdot (X\_i \- \\text{RTP})^2}$$

* $P\_i$: Probability of a specific winning combination.  
* $X\_i$: Payout multiplier for that combination (e.g., $10$ for a $10\\text{x}$ win).  
* $\\text{RTP}$: The total theoretical Return to Player (e.g., $0.96$ for $96\\%$). \[3, 4\]

### ---

**2\. Map to a 5-Star Scale \[5\]**

There is no single legal requirement for star mappings, but professional developers often use a **Weighted Volatility Score** (often out of 10\) and then divide by 2 to get stars. \[1, 2\]

A common industry formula for a **Volatility Score (0–10)** looks like this: \[1, 6\]

$$\\text{Score} \= (0.5 \\cdot \\text{Normalized SD}) \+ (0.3 \\cdot (1 \- \\text{Hit Frequency})) \+ (0.2 \\cdot \\text{Normalized Max Win})$$

| Volatility Level \[7, 8, 9, 10, 11\] | Star Rating | Typical SD Range | Characteristics |
| :---- | :---- | :---- | :---- |
| **Low** | ⭐ | $1.0 \- 3.0$ | Wins every 3–4 spins; small prizes. |
| **Low-Medium** | ⭐⭐ | $3.0 \- 5.0$ | Slightly more risk; occasional $50\\text{x}$ wins. |
| **Medium** | ⭐⭐⭐ | $5.0 \- 8.0$ | Balanced gameplay; the "industry standard". |
| **Medium-High** | ⭐⭐⭐⭐ | $8.0 \- 12.0$ | Fewer wins, but big "Mega Wins" are possible. |
| **High** | ⭐⭐⭐⭐⭐ | $12.0+$ | Long "dry spells" with huge jackpot potential. |

### ---

**3\. Key Factors for Your Model**

* **Bonus Features**: If your game has a "Free Spins" round that pays $500\\text{x}$ but only triggers every 150 spins, your volatility will naturally shift toward **4 or 5 stars**. \[12, 13\]  
* **Max Win Cap**: High caps (e.g., $5,000\\text{x}$ or $10,000\\text{x}$) significantly increase the standard deviation, pushing the star rating up. \[1, 6, 14\]  
* **Normalization**: To get your star rating, take your final **Score (0–10)** and assign it:  
  * $0–2 \= 1$ Star  
  * $2–4 \= 2$ Stars  
  * $4–6 \= 3$ Stars  
  * $6–8 \= 4$ Stars  
  * $8–10 \= 5$ Stars

### ---

**✅ Answer**

To calculate volatility for a 1–5 star rating, first determine the **Standard Deviation ($\\sigma$)** of your payout multipliers over a large sample (1M+ spins). Then, combine this with your **Hit Frequency** (how often any win occurs) and **Max Win** potential into a weighted scoring model. Map this final score to a 5-point scale based on the risk profile you want for your game. \[15\]

If you'd like, I can help you **refine the weights** for your specific game type. Tell me:

* What is your target **RTP** (e.g., $94\\%, 96\\%$)?  
* What is the **maximum multiplier** a player can win?  
* How often should the **bonus feature** trigger (e.g., 1 in 100 spins)?

\[1\] [https://www.scribd.com](https://www.scribd.com/document/862957476/slot-volatility-analysis)  
\[2\] [https://www.scribd.com](https://www.scribd.com/document/862957481/slot-volatility-analysis)  
\[3\] [https://havokjournal.com](https://havokjournal.com/uncategorized/decoding-slot-machine-mechanics-how-online-slots-for-money-really-work/#:~:text=RTP%20is%20a%20theoretical%20calculation%20that%20indicates,idea%20of%20the%20game%27s%20overall%20payout%20potential.)  
\[4\] [https://gamixlabs.com](https://gamixlabs.com/simulation.html#:~:text=Live%20Simulation%20Run%20%234092%20Theoretical%20RTP%20Return,spins%20that%20result%20in%20a%20non%2Dzero%20payout.)  
\[5\] [https://www.researchgate.net](https://www.researchgate.net/post/How-to-transform-standard-deviation-to-five-star-scale-slot-game-volatility)  
\[6\] [https://www.scribd.com](https://www.scribd.com/document/862957481/slot-volatility-analysis)  
\[7\] [https://mrq.com](https://mrq.com/blog/slot-volatility-explained)  
\[8\] [https://www.pokernews.com](https://www.pokernews.com/casino/slots/understanding-slots-volatility.htm)  
\[9\] [https://www.gammastack.com](https://www.gammastack.com/blog/using-volatility-and-rtp-to-attract-players-in-slots/)  
\[10\] [https://3d-elektronik.net](https://3d-elektronik.net/why-volatility-ratings-are-essential-for-every-punter-to-understand/)  
\[11\] [https://www.cachecreek.com](https://www.cachecreek.com/slot-machine-volatility)  
\[12\] [https://sigma.world](https://sigma.world/play/blog/what-does-volatility-mean-in-slots/)  
\[13\] [https://blr1.digitaloceanspaces.com](https://blr1.digitaloceanspaces.com/thejackpotjournal/slots/playslots/understanding-volatility-in-slot-games-what-you-need-to-know.html)  
\[14\] [https://purefloat.ca](https://purefloat.ca/plinko-volatility-rtp-guide/#:~:text=Max%20win%20tells%20you%20the%20ceiling%20of,a%20session%20will%20feel%20before%20you%20click.)  
\[15\] [https://javierbmartin.com](https://javierbmartin.com/rtp-in-online-slots-understanding-return-to-player-for-smarter-wins/#:~:text=Hit%20Frequency:%20Gauging%20Your%20Chances%20of%20Winning,those%20wins%20are%20smaller%20than%20your%20bet.)

## List of Possible Problems

High: the “strange” stats are real outputs of the model, not hidden behavior. The free-spin feature is parameterized to overpay badly. The free-spin multiplier distribution averages about 3.74x, and each trigger awards about 20.04 free spins on average before retriggers. In a 500k-spin run, about 1.81% of paid spins triggered free games, and each trigger expanded to about 33.37 total free spins after retriggers. That alone produced about 114.07% RTP from free games, for about 173.08% total RTP. Even with -wildsoff -expandoff, the code still returned about 93.91% total RTP, with free games alone contributing about 65.38%. The core problem is the feature math. Source: freeMultiplierDistribution and scatter distributions in src/Main.java:342-399.

Medium: retrigger staging looks wrong. During free spins, the code decides the next stage from freeGamesList.get(freeGamesList.size() - 1) instead of the currently played free spin. That can promote later-stage reels earlier than intended. It’s a real logic bug, but it does not appear to be the main reason the RTP is huge. Source: src/Main.java:734-756.

Low: Free Game RTP being over 100% is not inherently impossible here, because all RTP figures divide by paid-spin stake only. The actually implausible number is the 173% total RTP. Source: reporting code in src/Main.java:1084-1089.

Low: the printed Base Game Volatility is miscomputed, because it centers deviations on total RTP wonMoney / lostMoney instead of base RTP baseMoney / lostMoney. Source: src/Main.java:1133-1152.
