3 pillars that quietly govern almost all data-science work: 
a. Data Generating Process (DGP) 
b. Model Bias & Learning Behavior
c. Error, Uncertainty & Evaluation

I. Data Generating Process (DGP): Where data really comes from
Data is not truth. It's basically:
A proxy of reality
Filtered by business processes
Shaped by human decisions

Models don’t learn reality — they learn the rules that produced the data

Example (forecasting):
Sales data is influenced by:
a.Stock availability
b.Promotions
c. Sales team behavior
d. ERP cutoffs
e. Reporting delays

Key Intuition: So when a model “fails”, often:
The pattern changed or the process changed, not demand

II. Model Bias & Learning Behavior: How models think
Every model has preferences

a. Linear models: Prefer smooth, global relationships, Hate interactions unless told explicitly, Fail silently when assumptions break
b. Tree-based models (XGBoost, RF): Love splits & thresholds, Can model interactions naturally, Overfit patterns that don’t generalize
c. Time-series models (ARIMA): Assume past structure continues, Treat shocks as noise, Break badly on regime changes

Key intuition: A model’s failure mode is more important than its success case and choosing the model whose failure mode hurts least for the business.

III. Error, Uncertainty & Evaluation: What “good” really means

Most teams obsess over metrics, but miss the deeper layer.

Important distinctions:
Error ≠ Uncertainty
Low error doesn’t mean reliable
Stable error often matters more than minimal error

Forecasting intuition

A forecast is useful if:
-> It’s directionally right
-> It fails predictably
-> Stakeholders trust its behavior

A slightly worse MAE with:
-> Fewer extreme misses
-> Consistent bias
→ often wins in production

Key intuition: How wrong is acceptable — and when? An not How to make metrics better
-----------------------------------------------------------------------------------------------------------------

Model-Specific Intuition (Real-World Behavior)

I. Tree-Based Models (XGBoost intuition)
At its core, XGBoost: 
-> Keeps asking: “Where should I split to reduce error the most right now?” 
-> Learns conditional rules, not smooth equations
-> Stacks many small corrections
It's like If this AND this AND this, then adjust prediction by +x

Where it shines
-> Complex interactions
-> Non-linear effects 
-> Heterogeneous behavior across SKUs/customers

Where it silently fails
-> Sparse history - learns noise as signal
-> Leaky features - looks amazing, breaks in prod
-> Regime change - keeps trusting old splits


If XGBoost is great in backtest, weirdly confident, unstable for edge cases then
→ it’s probably memorizing structure that no longer exists.

II. Time-Series Models (ARIMA intuition)

ARIMA assumes:
-> The future is a transformation of the past
-> Shocks are temporary
-> Patterns repeat with noise