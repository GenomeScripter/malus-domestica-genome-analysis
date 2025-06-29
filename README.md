# 🍎 Apple Genome and Gene Expression Analysis

This project is part of a bioinformatics class assignment that uses Unix-based tools to analyze the genome and transcriptomic data of *Malus domestica* (apple). It simulates real-world genomics data exploration tasks using simplified, educational datasets.

---

## 📁 Project Files

- `apple.genome` – Apple genome sequences (modified from RGD).
- `apple.genes` – Gene annotation data: gene ID, transcript variant, chromosome, and strand.
- `apple.conditionA`, `apple.conditionB`, `apple.conditionC` – Gene expression data from RNA-seq experiments under three different tissue/conditions.

> **Note:** Data has been extracted and modified from the [Rosaceae Genome Database (RGD)](https://www.rosaceae.org) and may not directly reflect original RGD entries.

---

## 🖥️ Requirements

- A Unix-based operating system (Linux or macOS recommended)
- Standard command-line utilities: `grep`, `cut`, `sort`, `uniq`, `wc`, `comm`

---

## 🔬 Analysis Tasks

Each of the following questions was answered using shell command pipelines.

| #  | Question                                                                                  | Command Example                                                                 |
|----|-------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
| 1  | How many chromosomes are in the genome?                                                   | `grep ">" apple.genome \| wc -l`                                                |
| 2  | How many unique genes are there?                                                          | `cut -f1 apple.genes \| sort -u \| wc -l`                                       |
| 3  | How many transcript variants exist?                                                       | `cut -f2 apple.genes \| sort -u \| wc -l`                                       |
| 4  | How many genes have a single splice variant?                                              | `cut -f1 apple.genes \| sort \| uniq -c \| grep " 1 " \| wc -l`                 |
| 5  | How many genes have two or more splice variants?                                          | `cut -f1 apple.genes \| sort \| uniq -c \| grep -v " 1 " \| wc -l`              |
| 6  | How many genes are on the '+' strand?                                                     | `cut -f1,4 apple.genes \| grep "+" \| sort -u \| wc -l`                         |
| 7  | How many genes are on the '-' strand?                                                     | `cut -f1,4 apple.genes \| grep "-" \| uniq \| wc -l`                            |
| 8–10 | How many genes are on chr1, chr2, chr3 respectively?                                     | e.g., `cut -f1,3 apple.genes \| grep "chr1" \| uniq \| wc -l`                   |
| 11–13 | How many transcripts are on chr1, chr2, chr3 respectively?                               | e.g., `cut -f1,3 apple.genes \| grep "chr1" \| wc -l`                           |
| 14 | Genes in common between condition A and B                                                  | `comm -1 -2 A B \| wc -l`                                                       |
| 15 | Genes exclusive to condition A                                                            | `comm -2 -3 A BC \| wc -l`                                                      |
| 16 | Genes exclusive to condition B                                                            | `comm -2 -3 B AC \| wc -l`                                                      |
| 17 | Genes expressed in all three conditions                                                   | `cat A B C \| sort \| uniq -c \| grep " 3 " \| wc -l`                           |

> For questions 14–17, first prepare intermediate files:
```bash
cut -f1 apple.conditionA | sort -u > A
cut -f1 apple.conditionB | sort -u > B
cut -f1 apple.conditionC | sort -u > C
cat A C > AC
cat B C > BC


🧠 Learning Objectives
Practice Unix command-line operations for biological data processing

Understand gene structures, variants, and chromosomal organization

Perform RNA-seq condition comparisons using text-based file manipulations

📜 License
This project is intended for educational use only.
