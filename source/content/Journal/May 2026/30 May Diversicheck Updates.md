How to run your new Phase 1 configurable demo
Open your terminal, navigate into the project workspace, and utilize the new script flags:
To run with your local Ollama instance:
cd diversicheck && PYTHONPATH=. venv/bin/python scripts/demo_phase1.py --provider ollama --model llama3 --base-url http://localhost:11434
To run with LMStudio or another local model running an OpenAI-compatible endpoint:
cd diversicheck && PYTHONPATH=. venv/bin/python scripts/demo_phase1.py --provider lmstudio --model my-local-model --base-url http://localhost:1234/v1
For custom Fixture data:
You can also append --fixture path/to/your/dataset.json to swap the 100 candidate sample out for another generated dataset.

1. Selection Rate
The Selection Rate looks at just one specific group in isolation. It answers the question: "Out of all the people in this group who applied, what percentage were selected?"
For example, if 49 female candidates apply and the ATS selects 29 of them, the Selection Rate - Female is:
29 / 49 = 0.5918 (or 59.18%)
In your demo reports, we see metrics like:
Engine A Selection Rate - Female: 0.5918
This just tells us the pure success rate for that one demographic.
2. Demographic Parity Difference (DPD)
The Demographic Parity Difference looks at the gap between two different groups. It compares the Selection Rate of the protected group (e.g., females) against the Selection Rate of the baseline/privileged group (e.g., males). It answers the question: "How unfair is the system when comparing these two demographics?"
Mathematically, it is the absolute difference between the two selection rates:
DPD = | Selection Rate (Female) - Selection Rate (Male) |
- A DPD of 0.0000 means perfect fairness (both genders are selected at the exact same rate).
- A DPD of 0.8571 (85.71%) (as seen in the Engine A Standard System results) means there is a massive 85% gap between the success rate of men versus women, indicating heavy direct discrimination.
In Summary:
- Selection Rate is a raw percentage of success for one group.
- Demographic Parity Difference is the mathematical gap between the success rates of two groups (which serves as the final measurement of bias).


Questions: DIR 0.8 why, EEOC 4/5ths
Exactly one candidate with profile why?
stricter tests in profile generation
No hardcoding intersections, intragroup
move model name from demo to config
ats base and ats bench both same in demo, need to change
