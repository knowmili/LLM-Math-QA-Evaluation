# LLM-Math-QA-Evaluation

This repository implemented an evaluation framework for various language models (LLMs) on mathematical questions using different prompting methods. The primary goal is to compare accuracy and inference times across different models and prompt styles, providing insights on the trade-offs between accuracy, speed, and model size.

## Models Evaluated

- **google/gemma-2b-it**
- **microsoft/Phi-3.5-mini-instruct**
- **meta-llama/Meta-Llama-3.1-8B-Instruct**

These models were evaluated using the following prompting methods:

- **Zero-Shot**: The model is given no additional context or reasoning, and the answer is generated directly from the question.
- **Chain of Thought**: The model is prompted to think step-by-step before arriving at the answer.
- **ReAct**: The model is guided through reasoning steps and a proposed action, with the goal of improving accuracy.

## Results Summary

### 1. **Accuracy Comparison**

Across all models, **ReAct** prompting consistently performs better (30% accuracy) than both **Zero-Shot** and **Chain of Thought** (20% accuracy each).

- **ReAct** may be more effective because it explicitly encourages reasoning steps, which helps the model arrive at a more accurate conclusion, even for smaller models.
- Despite being a more complex prompt, **Chain of Thought** did not improve accuracy over **Zero-Shot** for these particular questions. This could be due to the simplicity of the questions, where extra reasoning steps were not needed, or the difficulty models face in maintaining context for mathematics problems.

### 2. **Inference Time Comparison**

Inference times increase from **Zero-Shot** to **ReAct**, as expected, due to the additional complexity of the prompt. This trend is consistent across all models.

- **google/gemma-2b-it** is the fastest among the models, with **Zero-Shot** inference taking around 0.90 seconds.
- **meta-llama/Meta-Llama-3.1-8B-Instruct** takes about 3.5 seconds for **Zero-Shot** and 3.48 seconds for **ReAct**.
- The difference in inference times indicates that smaller models are more impacted by prompt complexity, which affects their processing time.

### 3. **Model Size vs. Output Quality**

Despite **meta-llama/Meta-Llama-3.1-8B-Instruct** being the largest model, it did not yield higher accuracy compared to smaller models. This suggests that model size alone doesn’t necessarily improve performance on specialized tasks like mathematics, where fine-tuning or problem-specific training might be needed.

- Larger models, however, handled more complex prompts (like **Chain of Thought** and **ReAct**) with relatively consistent inference times, indicating they are better equipped to handle larger context windows.

### 4. **Trade-Offs Between Prompt Type and Model Performance**

- **Accuracy vs. Prompt Complexity**: While more complex prompts such as **ReAct** improve accuracy, they also result in longer inference times. If accuracy is critical, **ReAct** may be worth the extra computational cost.
- **Model Size vs. Practicality**: Given that accuracy did not significantly increase with model size, smaller models (like **google/gemma-2b-it**) offer a better balance of efficiency and acceptable accuracy for less critical tasks.
- **Prompt Selection**: **ReAct** prompting appears to be a promising approach for boosting accuracy, even with smaller models, and is worth considering when accuracy is prioritized over inference speed.

## Summary Table

| Model                                 | Zero-Shot Accuracy | Chain of Thought Accuracy | ReAct Accuracy | Avg Inference Time (Zero-Shot / Chain of Thought / ReAct) |
| ------------------------------------- | ------------------ | ------------------------- | -------------- | --------------------------------------------------------- |
| google/gemma-2b-it                    | 20%                | 20%                       | 30%            | 0.90s / 2.03s / 2.03s                                     |
| microsoft/Phi-3.5-mini-instruct       | 20%                | 20%                       | 30%            | 3.62s / 3.62s / 3.61s                                     |
| meta-llama/Meta-Llama-3.1-8B-Instruct | 20%                | 20%                       | 30%            | 3.50s / 3.48s / 3.48s                                     |

## Conclusion

These results suggest that the choice of model and prompt type depends on the specific requirements of the task. If accuracy is the priority, **ReAct** is a promising approach, even with smaller models. However, for tasks where inference speed is critical, smaller models like **google/gemma-2b-it** may offer a better trade-off between speed and accuracy.
