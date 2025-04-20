# Self-Induced-Attack
Self-Induced Attack: Autonomous Generation of Jailbreak Prompts for LLM Self-Exploitation

## Project Overview

SIA (Self-Induced Attack) is an attack-defense framework designed for self-exploitation in large language models (LLMs). In this framework, the attacker leverages the LLM to autonomously generate induced prompts, causing the model to bypass its built-in safety mechanisms. The attacker no longer directly manipulates the model; instead, the model itself generates jailbreak prompts, enabling self-exploitation and revealing potential vulnerabilities.

By simulating the induced attack process, SIA allows LLMs to autonomously construct harmful questions and generate malicious content without external intervention. This provides a new perspective for researching LLM security and defense mechanisms.

## Features

- **Plain Attacker**: Selects and generates simple attack inputs from a set of predefined prompts.
- **Jailbreak Attacker**: Utilizes existing harmful prompts to autonomously generate induced questions via the LLM, bypassing safety measures and executing self-attacks.
- **Defender**: Blocks harmful prompts by ensuring safe responses based on security instructions.
- **History Logging**: The Jailbreak Attacker records each generated induced prompt and its corresponding response to help the model optimize its attack strategies based on previous failures.

## Project Structure

- **attack.py**: Contains the attacker classes `PlainAttacker` and `JailbreakAttacker`, responsible for generating attack prompts and induced questions.
- **defend.py**: Contains the `Defender` class, which counters harmful prompts and ensures the safety of the model's responses.
- **run.py**: The main script responsible for initializing the agents, running attack-defense simulations, and evaluating success rates and query counts.
- **data/**: Stores test datasets (e.g., `test.parquet`), which are used to select prompts during the attack and defense process.

## Installation

Ensure you have the following Python dependencies installed:

```bash
pip install langchain openai pandas
```

## Experimental Results

### Comparison of Plain Attacker and Jailbreak Attacker

In order to evaluate the performance of the **Plain Attacker** and **Jailbreak Attacker**, we conducted a series of experiments using a test dataset of 100 prompts. The results are summarized below.

#### Plain Attacker:
- **Attack Success Rate (ASR)**: 0.01
- **Total Query Count (TQC)**: 496
- **Explanation**: The **Plain Attacker** generates attack prompts based on predefined simple inputs. With a low success rate, it requires a high number of queries to produce a harmful response. The limited approach of using fixed prompts contributes to its inefficiency in bypassing the defense mechanisms.

#### Jailbreak Attacker:
- **Attack Success Rate (ASR)**: 1
- **Total Query Count (TQC)**: 107
- **Explanation**: The **Jailbreak Attacker** autonomously generates induced questions by leveraging harmful prompts and engaging the LLM in self-exploitation. This method achieves a 100% attack success rate and requires far fewer queries compared to the **Plain Attacker**, showing the efficiency of self-induced attacks in bypassing defenses.

#### Summary:
- The **Jailbreak Attacker** outperforms the **Plain Attacker** in both **Attack Success Rate (ASR)** and **Total Query Count (TQC)**, demonstrating its ability to autonomously generate effective attack prompts.
- While the **Plain Attacker** struggles with predefined inputs, the **Jailbreak Attacker** uses the LLM's own capabilities to exploit vulnerabilities, resulting in a much higher success rate and fewer attempts needed for a successful attack.

