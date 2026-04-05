# fq-manifestor

A browser-based tool for generating [QIIME 2 paired-end fastq manifest files](https://docs.qiime2.org/2022.2/tutorials/importing/#fastq-manifest-formats) from a directory of demultiplexed Illumina FASTQ files.

No installation required. Works entirely in the browser — nothing is uploaded.

## Usage

**Online:** visit the hosted version at [gregcaporaso.github.io/fq-manifestor-web](https://gregcaporaso.github.io/fq-manifestor-web).

**Offline:** download `index.html` and open it in any browser.

### Workflow

1. Drop your top-level FASTQ folder into the drop zone (or click Browse)
2. Adjust the pattern options if your files use different naming conventions
3. Download the manifest and move it into the folder you dropped
4. `cd` into that folder and run the QIIME 2 import command shown on the page

### Why `cd` into the folder first?

The manifest uses `$PWD` in place of the absolute base path, which the shell expands to the current working directory when you run the import command. Running from the FASTQ folder means `$PWD` resolves to the correct path automatically — no editing of the manifest needed.

## Input data format

The tool searches the dropped folder recursively for FASTQ files. For each file it splits the filename on the split pattern (default `_`) and takes the text before the first match as the sample ID. It then matches forward and reverse reads using the R1/R2 patterns.

Example directory structure (defaults work for this layout):

```text
humanure-run1/
├── 07717ac5_L001-ds.079/
│   ├── 07717ac5_S71_L001_R1_001.fastq.gz
│   └── 07717ac5_S71_L001_R2_001.fastq.gz
├── 08a10d08_L001-ds.060/
│   ├── 08a10d08_S30_L001_R1_001.fastq.gz
│   └── 08a10d08_S30_L001_R2_001.fastq.gz
```

Sample IDs for the above would be `07717ac5` and `08a10d08`.

## Issues

Please report problems on the [issue tracker](https://github.com/gregcaporaso/fq-manifestor/issues).
