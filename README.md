# Scaling AI-Driven Market Share Estimation to Production

**Bachelor's Thesis — Artificial Intelligence, Universitat Politècnica de Catalunya (UPC)**
Joan Bennàssar Martín · Grade: 9/10 · June 2026

Developed during an internship at [Shalion](https://www.shalion.com), a Barcelona-based e-commerce analytics company, as part of the launch of their Retail Media Maestro product.

## About

This thesis documents the scaling of an AI-driven market share estimation service from a functional prototype to a production system running weekly for real clients. The pipeline infers product- and brand-level market share from public digital shelf signals (Best Seller Rankings, units-sold indicators, reviews, ratings) and confidential Amazon Vendor Central data where available.

At the volume required for production (20,000+ seeds, 4 major US retailers), the original system took more than 12 hours and did not complete, due to a Snowflake queuing bottleneck caused by 500,000+ individual database reads per run. This work redesigns the architecture to reduce that to a single bulk query per client batch, bringing the full weekly run down to **~1 hour**.

**Key contributions:**
- Two-stage architectural redesign of the data collection pipeline, eliminating the Snowflake read bottleneck (execution time: +12h timeout → ~1 hour)
- A nine-tier routing system assigning each product to the most appropriate estimation pipeline based on available signals
- Two new XGBoost pipelines for non-Amazon retailers and rank-only products, reducing held-out WMAPE from 101% → 46% and 115% → 63%
- A revenue proxy method (based on weekly review deltas) to aggregate market share estimates across category levels, empirically validated
- A migration design for output storage to Apache Iceberg tables

**Supervisors:** Ramon Sangüesa Solé (UPC) · Magdalena Sztandarska (Shalion Data Services SL)

## Contents

- [`TFG-JoanBennassarMartin.pdf`](./TFG-JoanBennassarMartin.pdf) — Full thesis document
- [`TFG-slides.pdf`](./TFG-slides.pdf.pdf) — Defense presentation slides

## Abstract

This thesis describes the scaling of an AI-driven market share estimation service from a functional prototype to a production system running weekly for real clients. The work was carried out during an internship at Shalion, a Barcelona-based e-commerce analytics company, in the context of the launch of the Retail Media Maestro product, whose Marketshare module lets clients view estimates across the four most important US retailers, covering more than 20,000 seeds.

The starting point was a modular pipeline that infers product- and brand-level market share from public digital shelf signals — Best Seller Rankings, units-sold indicators, reviews, and ratings — and from confidential Amazon Vendor Central actuals where available. At the seed volume required by the new product, the system took more than 12 hours each week and did not complete, due to a Snowflake queuing problem caused by more than 500,000 individual database reads per execution. The primary engineering contribution of this thesis is the elimination of this bottleneck through a two-stage architectural redesign that reduces total reads to a single bulk query per client batch. As a result, the full weekly run completes in approximately one hour, where previously it did not finish at all.

In parallel, the modelling layer was extended with a nine-tier routing system and two new XGBoost pipelines, substantially improving estimation accuracy for non-Amazon retailers and low-signal products. A revenue proxy for aggregating estimates across category levels was also developed and empirically validated.

## Tech Stack

Python · XGBoost · Optuna · Apache Airflow · AWS ECS/Fargate · Snowflake · Apache Iceberg · dbt

## Contact

Joan Bennàssar Martín
[LinkedIn](https://www.linkedin.com/in/joan-bennassar-martin/) · janben2004@gmail.com
