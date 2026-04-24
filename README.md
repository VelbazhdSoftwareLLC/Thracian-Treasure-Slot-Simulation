# Thracian Treasure Slot Simulation

Slot machine game simulation.

javac Main.java

java Main -help

java Main -g100m -p10k

java Main -verify

# List of Possible Problems

High: the “strange” stats are real outputs of the model, not hidden behavior. The free-spin feature is parameterized to overpay badly. The free-spin multiplier distribution averages about 3.74x, and each trigger awards about 20.04 free spins on average before retriggers. In a 500k-spin run, about 1.81% of paid spins triggered free games, and each trigger expanded to about 33.37 total free spins after retriggers. That alone produced about 114.07% RTP from free games, for about 173.08% total RTP. Even with -wildsoff -expandoff, the code still returned about 93.91% total RTP, with free games alone contributing about 65.38%. The core problem is the feature math. Source: freeMultiplierDistribution and scatter distributions in src/Main.java:342-399.

Medium: retrigger staging looks wrong. During free spins, the code decides the next stage from freeGamesList.get(freeGamesList.size() - 1) instead of the currently played free spin. That can promote later-stage reels earlier than intended. It’s a real logic bug, but it does not appear to be the main reason the RTP is huge. Source: src/Main.java:734-756.

Low: Free Game RTP being over 100% is not inherently impossible here, because all RTP figures divide by paid-spin stake only. The actually implausible number is the 173% total RTP. Source: reporting code in src/Main.java:1084-1089.

Low: the printed Base Game Volatility is miscomputed, because it centers deviations on total RTP wonMoney / lostMoney instead of base RTP baseMoney / lostMoney. Source: src/Main.java:1133-1152.
