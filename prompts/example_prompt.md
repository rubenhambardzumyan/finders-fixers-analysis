Task: Your task is to apply Finder and Fixer prompts on each BrainLift located in the @brainlifts/ directory.

Input files:

- BrainLifts to process: Read from brainlifts/brainlift_1.md, brainlifts/brainlift_2.md, etc.
- Finder prompts: Read from finders/v1/ directory
- Fixer prompts: Read from fixers/v1/ directory
- Context: Read from context/brainlift-definition.md

Output:

- Create files in the existing @outcome/vN-vM/ directory, where vN is the version folder of Finders, and vM for fixers. For example: v1-v1
- Name them brainlift_outcome_X.md (where X matches the brainlift number)