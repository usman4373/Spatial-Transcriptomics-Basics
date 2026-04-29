# 1. What is Spatial scRNA Transcriptomics?

Spatial transcriptomics refers to technologies that measure gene expression while preserving the spatial location of cells within tissue

It combines:
- Single-cell RNA sequencing (who is expressing what)
- Spatial information (where it is happening)

In contrast:
- Traditional scRNA-seq → loses positional information
- Spatial transcriptomics → keeps tissue architecture intact

---

# Core Concept

Each data point is not just:

`Cell → Gene expression`

But:

`Cell/Spot → Gene expression + (x, y coordinates) + tissue context`



# 2. Major Divisions of Spatial Transcriptomics

Spatial transcriptomics broadly falls into two main categories:

A. Imaging-Based Methods
B. Sequencing-Based Methods

## A. Imaging-Based Methods

These rely on microscopy + labeled probes

**Key Features:**
- Direct visualization in tissue
- High spatial resolution (often single-cell or subcellular)
- Usually targeted gene panels

**Types of Imaging-Based Methods**

1. smFISH-based (single-molecule FISH)
- Detects individual RNA molecules
- High accuracy, low multiplexing (initially)

Examples:
- MERFISH
- seqFISH

2. In situ sequencing
- Sequencing happens directly in tissue

Example:
- ISS

**Pros**
- Single-cell / subcellular resolution
- Precise spatial localization

**Cons**
- Limited number of genes (compared to sequencing-based methods)
- Expensive and technically complex



























