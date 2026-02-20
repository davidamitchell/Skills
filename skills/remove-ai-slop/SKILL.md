---
name: remove-ai-slop
description: Systematically removes AI detection signals from text — statistical,
  structural, rhetorical, and alignment-induced patterns. Use when asked to humanize
  text, eliminate AI slop, reduce AI detection probability, or clean AI-generated
  content of its characteristic fingerprints.
scope: "Post-generation transformation and signal suppression"
priority: "Stealth over stylistic optimization"
---

# Skill: AI Slop Elimination & Signal Suppression

## Purpose

Systematically remove statistical, structural, rhetorical, and alignment-induced signals that increase the probability a text is classified as AI-generated.

This skill operates post-generation and focuses on **distributional disruption**, **pattern irregularization**, and **detector surface minimization**.
Stylistic human-authentic voice is handled elsewhere.

---

## 0. Threat Model

AI detection systems typically rely on one or more of:

1. **Perplexity-based metrics**
   - Low entropy / overly probable token sequences
   - Predictable transitions
2. **Classifier-based detectors**
   - Fine-tuned neural classifiers trained on RLHF outputs
3. **Curvature-based detection**
   - Sensitivity to log-probability perturbation
4. **Stylometric fingerprinting**
   - Sentence uniformity
   - Transition markers
   - Hedging patterns
5. **Watermark schemes**
   - Biased token sampling
6. **Alignment artifacts**
   - Over-clarity
   - Over-structure
   - Safe phrasing

Goal: Reduce statistical regularity and alignment signatures without introducing incoherence.

---

## 1. Signal Decomposition

### 1.1 Core AI Slop Features

Break text into atomic detectable features:

- Repetitive clause structure
- Predictable paragraph architecture
- Excessive explicit transitions
- Overly balanced sentence length
- Uniform syntactic rhythm
- Hedging density
- Safety disclaimers
- Explicit meta-structure ("In conclusion", "This means that")
- High semantic density without human noise
- Polished coherence with no micro-disruptions

---

## 2. Recursive Slop Removal Algorithm
