# Spatial Transcriptomics Basics

<p style="text-align: justify;">This repository provides a beginner-friendly introduction to spatial transcriptomics for researchers transitioning from standard single-cell RNA-seq. It explains core concepts, major technologies, and key analytical workflows used in spatial data analysis. The guide also highlights common pitfalls and important conceptual shifts required when working with spatially resolved gene expression data. It is designed as a quick but solid foundation for understanding and analyzing spatial transcriptomics datasets.</p>

## Table of Contents

1. [What is Spatial scRNA Transcriptomics?](#1-what-is-spatial-scrna-transcriptomics)
2. [Major Divisions of Spatial Transcriptomics](#2-major-divisions-of-spatial-transcriptomics)
3. [Summary of Major Platforms](#3-summary-of-major-platforms)
4. [Typical Spatial Transcriptomics Workflow](#4-typical-spatial-transcriptomics-workflow)
5. [Critical Things to Keep in Mind](#5-critical-things-to-keep-in-mind-this-is-where-people-mess-up)
6. [Conceptual Shift You Must Internalize](#6-conceptual-shift-you-must-internalize)
7. [Why the “merge-first” approach breaks in spatial data](#7-why-the-merge-first-approach-breaks-in-spatial-data)

---

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

---

# 5. Critical Things to Keep in Mind (THIS IS WHERE PEOPLE MESS UP)

### 1. Spatial ≠ Single-cell (always)
- Visium spots ≠ single cells
- Always consider mixed cell populations

### 2. Do NOT blindly merge samples
- Each sample has its own spatial architecture
- Merging destroys biological spatial patterns

### 3. Batch effects are different here
- Technical + spatial + biological variation are intertwined
- Overcorrection can remove real spatial biology

### 4. Histology matters
- Always overlay gene expression on tissue image
- Ignoring morphology = missing half the story

### 5. Resolution limitations
- Know your platform resolution
- Don’t overinterpret spot-level data as single-cell

### 6. Deconvolution is not optional (for many datasets)
- Especially for 10x Genomics Visium

### 7. Spatial statistics are different
- You need methods that account for spatial structure:
  - Moran’s I
  - Geary’s C

### 8. Integration with scRNA-seq is key
- Spatial data often needs:
  - Reference scRNA-seq datasets
  - Label transfer

---

# 6. Conceptual Shift You Must Internalize

This is the biggest mindset change:
- In scRNA-seq:
  - Cells are independent
- In spatial transcriptomics:
  - Cells are context-dependent and spatially correlated

---

# 7. Why the “merge-first” approach breaks in spatial data
- In traditional scRNA-seq, merging datasets (with batch correction) is often fine because cells are assumed to be independent observations
- But spatial data introduces an extra layer: location matters
- If you merge everything blindly:
  - You lose spatial context, which is the whole point of spatial assays
  - You risk mixing biological spatial heterogeneity (real tissue structure) with technical variation
  - You may distort cell–cell interaction patterns, since proximity relationships differ across samples
  - You ignore sample-specific architecture (e.g., tumor margins vs core, tissue layers)

So, unlike standard scRNA-seq, samples are not just batches—they are distinct spatial systems

## What makes spatial data fundamentally different
- Spatial transcriptomics sits at the intersection of:
  - Single-cell RNA sequencing
  - And spatial biology (tissue architecture, microenvironment)
- Each sample encodes:
  - Gene expression
  - Coordinates (x, y)
  - Often morphology (histology images)

Merging without respecting coordinates is like combining multiple maps and ignoring geography.

## When merging can be appropriate
- It’s not that merging is always wrong. It’s about how and when

**Acceptable scenarios:**
- After within-sample preprocessing
- Using methods designed for spatial integration (not naive concatenation)
- When aligning shared biological signals, not spatial structure
- For cell-type annotation transfer or reference mapping

**Common strategies:**
- Analyze each sample separately first
- Identify shared features (cell types, gene programs)
- Then integrate using spatial-aware or batch-aware methods

> Blindly merging spatial datasets like traditional scRNA-seq is methodologically flawed. But careful, purpose-driven integration is still valid and often necessary

---
