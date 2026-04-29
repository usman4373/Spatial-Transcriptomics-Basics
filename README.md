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

---

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

## B. Sequencing-Based Methods

These capture RNA and sequence it like scRNA-seq, but with spatial barcodes

**Key Features:**
- Genome-wide or near genome-wide expression
- Lower spatial resolution (spot-based in many cases)

**Types of Sequencing-Based Methods**

1. Spot-based (capture arrays)
- Tissue placed on barcoded slide
- Each spot captures transcripts from nearby cells

Example:
- 10x Genomics Visium
> Each “spot” may contain multiple cells

2. Bead-based / high-resolution arrays
- Randomly distributed barcoded beads
- Higher resolution than Visium

Examples:
- Slide-seq
- HDST

3. Laser capture / microdissection
- Physically isolate regions before sequencing

Example:
- LCM-seq

**Pros**
- Transcriptome-wide
- Compatible with scRNA-seq pipelines

**Cons**
- Lower spatial resolution
- Spot-level mixing of cells

---

# 3. Summary of Major Platforms

Here’s how commonly used platforms compare:

**Imaging-based**
- MERFISH → very high multiplexing, single-cell
- seqFISH → spatial gene panels

**Sequencing-based**
- 10x Genomics Visium → ~55 µm spots, widely used
- Slide-seq → higher resolution (~10 µm)
- HDST → even finer resolution

---

# 4. Typical Spatial Transcriptomics Workflow

## Step 1: Experimental Setup
- Tissue collection (fresh frozen or FFPE)
- Sectioning
- Placement on spatial slide

## Step 2: Data Generation
- RNA capture
- Barcode assignment
- Sequencing or imaging

## Step 3: Preprocessing
- Alignment
- Count matrix generation
- Spatial coordinate mapping

## Step 4: Quality Control (VERY IMPORTANT)
- Check:
  - Low-quality spots
  - RNA counts per spot
  - mitochondrial gene percentage

## Step 5: Normalization
- Must consider:
  - Spot-level variation
  - technical noise

## Step 6: Downstream Analysis

**A. Clustering**
- Identify spatial domains

**B. Spatial domain detection**
- Regions with similar expression patterns

**C. Cell type annotation**
- Often via mapping to scRNA-seq references

**D. Deconvolution (for spot-based data)**
- Estimate cell-type composition per spot

**E. Spatially variable genes**
- Genes whose expression depends on location

**F. Cell–cell interaction analysis**
- Ligand–receptor analysis with spatial constraints





























