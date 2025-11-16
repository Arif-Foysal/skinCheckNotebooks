# Methodology Flowchart: Architecture-Specific Preprocessing Optimization

## Visual Flowchart Design

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           METHODOLOGY FLOWCHART                                 │
│            Architecture-Specific Preprocessing Optimization Study               │
└─────────────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                              PHASE 1: SETUP                                    │
└─────────────────────────────────────────────────────────────────────────────────┘

                          ┌─────────────────────────┐
                          │     HAM10000 Dataset   │
                          │    (10,015 images)     │
                          └──────────┬──────────────┘
                                     │
                                     ▼
                          ┌─────────────────────────┐
                          │   Dataset Filtering     │
                          │  Binary Classification  │
                          │   (Benign vs Malignant) │
                          └──────────┬──────────────┘
                                     │
                                     ▼
                          ┌─────────────────────────┐
                          │   Final Dataset:       │
                          │   2,013 images         │
                          │   (Balanced classes)    │
                          └──────────┬──────────────┘
                                     │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                        PHASE 2: ARCHITECTURE SELECTION                         │
└─────────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
                          ┌─────────────────────────┐
                          │  Preliminary Benchmark │
                          │    4 SOTA Models:      │
                          │  • Vision Transformer  │
                          │  • Swin Transformer    │
                          │  • ResNet50            │
                          │  • EfficientNet-B0     │
                          └──────────┬──────────────┘
                                     │
                                     ▼
                          ┌─────────────────────────┐
                          │   Architecture         │
                          │   Selection Results:    │
                          │   • ViT: Best Overall   │
                          │   • ResNet50: Best CNN │
                          └──────────┬──────────────┘
                                     │
┌─────────────────────────────────────────────────────────────────────────────────┐
│                     PHASE 3: PREPROCESSING CONFIGURATIONS                      │
└─────────────────────────────────────────────────────────────────────────────────┘
                                     │
                                     ▼
                    ┌─────────────────────────────────────────────┐
                    │          7 PREPROCESSING CONFIGURATIONS      │
                    └─────────────────┬───────────────────────────┘
                                      │
              ┌───────────────────────┼───────────────────────┐
              │                       │                       │
              ▼                       ▼                       ▼
    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │   BASELINE      │    │   INDIVIDUAL    │    │   COMBINED      │
    │                 │    │   TECHNIQUES    │    │   TECHNIQUES    │
    │ C1: No          │    │                 │    │                 │
    │ Preprocessing   │    │ C2: Hair        │    │ C5: Hair +      │
    │                 │    │     Removal     │    │     Noise       │
    │ • Raw images    │    │                 │    │                 │
    │ • Resize only   │    │ C3: Noise       │    │ C6: Hair +      │
    │ • Normalize     │    │     Reduction   │    │     Segmentation│
    └─────────────────┘    │                 │    │                 │
                           │ C4: Ground      │    │ C7: Full        │
                           │     Truth       │    │     Pipeline    │
                           │     Segmentation│    │     (All 3)     │
                           └─────────────────┘    └─────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                     PHASE 4: EXPERIMENTAL EXECUTION                            │
└─────────────────────────────────────────────────────────────────────────────────┘

                    ┌─────────────────────────────────────────────┐
                    │         SYSTEMATIC EVALUATION               │
                    │      (2 Architectures × 7 Configurations)  │
                    └─────────────────┬───────────────────────────┘
                                      │
              ┌───────────────────────┼───────────────────────┐
              │                       │                       │
              ▼                       ▼                       ▼
    ┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
    │   ResNet50      │    │   Vision        │    │   TRAINING      │
    │   EXPERIMENTS   │    │   Transformer   │    │   PROTOCOL      │
    │                 │    │   EXPERIMENTS   │    │                 │
    │ • 7 configs     │    │                 │    │ • Batch: 16     │
    │ • 2-fold CV     │    │ • 7 configs     │    │ • LR: 1e-6      │
    │ • Identical     │    │ • 2-fold CV     │    │ • Epochs: 5     │
    │   parameters    │    │ • Identical     │    │ • Adam Opt      │
    │                 │    │   parameters    │    │ • Weight decay  │
    └─────────────────┘    └─────────────────┘    └─────────────────┘
              │                       │                       │
              └───────────────────────┼───────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │            TOTAL EXPERIMENTS:               │
                    │        2 Architectures × 7 Configs         │
                    │           = 14 Experiments                  │
                    │        Each with 2-fold CV                 │
                    │           = 28 Training Runs               │
                    └─────────────────┬───────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                      PHASE 5: STATISTICAL ANALYSIS                             │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │         PERFORMANCE METRICS                 │
                    │                                             │
                    │ Primary: Accuracy (Mean ± SD)              │
                    │ Secondary: Precision, Recall, F1, AUC      │
                    └─────────────────┬───────────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │        STATISTICAL TESTING                  │
                    │                                             │
                    │ • Paired t-tests (config comparisons)      │
                    │ • Bonferroni correction (multiple comp.)   │
                    │ • Cohen's d (effect size calculation)      │
                    │ • Significance threshold: p < 0.05         │
                    └─────────────────┬───────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                         PHASE 6: RESULTS & ANALYSIS                            │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
              ┌───────────────────────┴───────────────────────┐
              │                                               │
              ▼                                               ▼
    ┌─────────────────┐                            ┌─────────────────┐
    │   ResNet50      │                            │   Vision        │
    │   RESULTS       │                            │   Transformer   │
    │                 │                            │   RESULTS       │
    │ Best: C3        │                            │                 │
    │ (Noise Reduction)│                            │ Best: C4        │
    │ 85.07% (+3.10%) │                            │ (Segmentation)  │
    │                 │                            │ 83.03% (+8.09%) │
    └─────────────────┘                            └─────────────────┘
              │                                               │
              └───────────────────────┬───────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │        KEY FINDINGS                         │
                    │                                             │
                    │ ✓ Architecture-specific preprocessing       │
                    │ ✓ Individual > Combined techniques          │
                    │ ✓ Simple often beats complex               │
                    │ ✓ Clinical deployment implications         │
                    └─────────────────┬───────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────────────┐
│                           PHASE 7: VALIDATION                                  │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │      MODEL VALIDATION CHECKS               │
                    │                                             │
                    │ • Cross-validation consistency             │
                    │ • Error analysis and failure cases         │
                    │ • Preprocessing pipeline verification      │
                    │ • Statistical assumption validation        │
                    └─────────────────┬───────────────────────────┘
                                      │
                                      ▼
                    ┌─────────────────────────────────────────────┐
                    │         CLINICAL TRANSLATION                │
                    │                                             │
                    │ • Deployment guidelines                     │
                    │ • Resource allocation recommendations       │
                    │ • Architecture selection criteria          │
                    │ • Cost-benefit analysis                     │
                    └─────────────────────────────────────────────┘
```

## Detailed Component Descriptions

### Phase 1: Dataset Preparation
```
HAM10000 Dataset (10,015 images)
         ↓
Binary Classification Filter
(Benign: nv, bkl, df, vasc)
(Malignant: mel, bcc, akiec)
         ↓
Final Dataset: 2,013 images
(Balanced distribution)
```

### Phase 2: Architecture Selection Matrix
```
┌─────────────────┬─────────────┬─────────────┬─────────────┐
│ Model           │ Baseline    │ Architecture│ Selection   │
│                 │ Accuracy    │ Type        │ Status      │
├─────────────────┼─────────────┼─────────────┼─────────────┤
│ Vision Trans.   │ 74.94%      │ Attention   │ ✓ Selected  │
│ Swin Trans.     │ [Benchmark] │ Attention   │ ○ Future    │
│ ResNet50        │ 81.97%      │ CNN         │ ✓ Selected  │
│ EfficientNet    │ [Benchmark] │ CNN         │ ○ Excluded  │
└─────────────────┴─────────────┴─────────────┴─────────────┘
```

### Phase 3: Preprocessing Configuration Matrix
```
┌──────────┬─────────────┬─────────────┬─────────────┬─────────────┐
│ Config   │ Hair        │ Noise       │ Ground      │ Description │
│          │ Removal     │ Reduction   │ Truth Seg   │             │
├──────────┼─────────────┼─────────────┼─────────────┼─────────────┤
│ C1       │ ✗           │ ✗           │ ✗           │ Baseline    │
│ C2       │ ✓           │ ✗           │ ✗           │ Individual  │
│ C3       │ ✗           │ ✓           │ ✗           │ Individual  │
│ C4       │ ✗           │ ✗           │ ✓           │ Individual  │
│ C5       │ ✓           │ ✓           │ ✗           │ Combined    │
│ C6       │ ✓           │ ✗           │ ✓           │ Combined    │
│ C7       │ ✓           │ ✓           │ ✓           │ Full        │
└──────────┴─────────────┴─────────────┴─────────────┴─────────────┘
```

### Phase 4: Experimental Design Flow
```
Training Protocol Consistency:
┌─────────────────────────────────────────┐
│ Hyperparameter    │ Value               │
├─────────────────────────────────────────┤
│ Batch Size        │ 16                  │
│ Learning Rate     │ 1e-6                │
│ Optimizer         │ Adam                │
│ Epochs            │ 5                   │
│ Cross-Validation  │ 2-fold Stratified   │
│ Hardware          │ NVIDIA GPU + CUDA   │
└─────────────────────────────────────────┘
```

### Phase 5: Statistical Analysis Pipeline
```
Raw Results
     ↓
Performance Metrics Calculation
(Accuracy, Precision, Recall, F1, AUC)
     ↓
Statistical Testing
     ├── Paired t-tests (within architecture)
     ├── Effect size calculation (Cohen's d)
     └── Multiple comparison correction
     ↓
Significance Assessment
(p < 0.05 threshold)
     ↓
Clinical Significance Evaluation
(Effect size interpretation)
```

### Phase 6: Results Analysis Framework
```
Architecture-Specific Analysis:
┌─────────────────────────────────────────┐
│           ResNet50 Results              │
│  ┌─────────┬──────────┬─────────────┐   │
│  │ Config  │ Accuracy │ Improvement │   │
│  ├─────────┼──────────┼─────────────┤   │
│  │ C1      │ 81.97%   │ Baseline    │   │
│  │ C3      │ 85.07%   │ +3.10%      │   │
│  │ C7      │ 78.53%   │ -3.44%      │   │
│  └─────────┴──────────┴─────────────┘   │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│        Vision Transformer Results       │
│  ┌─────────┬──────────┬─────────────┐   │
│  │ Config  │ Accuracy │ Improvement │   │
│  ├─────────┼──────────┼─────────────┤   │
│  │ C1      │ 74.94%   │ Baseline    │   │
│  │ C4      │ 83.03%   │ +8.09%      │   │
│  │ C7      │ 82.23%   │ +7.29%      │   │
│  └─────────┴──────────┴─────────────┘   │
└─────────────────────────────────────────┘
```

## Implementation Notes for Visual Creation

### For PowerPoint/Keynote:
1. **Use SmartArt** - Process flow diagrams work well
2. **Color Coding**:
   - Blue: Data/Dataset phases
   - Green: Methodology phases  
   - Orange: Analysis phases
   - Red: Results phases
3. **Icons**: Use medical, AI, and process icons
4. **Arrows**: Consistent flow direction (top to bottom)

### For Draw.io/Lucidchart:
1. **Swimlane Diagram** - Separate phases into horizontal lanes
2. **Decision Points** - Diamond shapes for selection criteria
3. **Process Boxes** - Rectangles for each major step
4. **Data Stores** - Cylinders for datasets

### For LaTeX/TikZ:
```latex
\usepackage{tikz}
\usetikzlibrary{shapes,arrows,positioning}
% Define styles for different node types
\tikzstyle{data} = [rectangle, draw, fill=blue!20]
\tikzstyle{process} = [rectangle, draw, fill=green!20]
\tikzstyle{analysis} = [rectangle, draw, fill=orange!20]
\tikzstyle{results} = [rectangle, draw, fill=red!20]
```

## Key Visual Elements to Emphasize

1. **Systematic Nature** - Show parallel processing of both architectures
2. **Configuration Matrix** - Clear table showing all 7 combinations
3. **Decision Points** - Why specific architectures were selected
4. **Statistical Rigor** - Highlight cross-validation and testing
5. **Clinical Translation** - End with deployment implications

This flowchart visually demonstrates the systematic, rigorous approach of your methodology while making it easy for audiences to follow your experimental logic.
