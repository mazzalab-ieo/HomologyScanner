# Homology Scanner

Homology Scanner is a Python script that calculates the homology level of genomic positions on an input sequence, aiding in the analysis of read mismapping probabilities. The script utilizes sequence alignment tools and provides various modes of operation for generating reads, introducing mutations, and computing homology scores.

## Table of Contents

- [Introduction](#introduction)
- [Installation](#installation)
- [Usage](#usage)
- [Command-line Arguments](#command-line-arguments)
- [Examples](#examples)
- [Contributing](#contributing)
- [License](#license)

## Introduction

This program calculates the homology level of genomic positions on an input sequence (in FASTA format) and a window around the position, generating a score that indicates the probability of read mismapping. The homology level is calculated using the output of BLAT (Conda version). The program also supports a simulation mode for generating reads at specific positions and introducing random mutations.

The script accepts command-line arguments to specify the input parameters, such as the reference genome file, window size, input file, chromosome, position, output file prefixes, and various operation modes.

## Installation

1. Clone the repository:

   ```bash
   git clone https://github.com/your-username/homology-scanner.git
   ```

2. Change into the project directory:

   ```bash
   cd homology-scanner
   ```

3. Install the required dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. You're ready to use the Homology Scanner!

## Usage

To use the Homology Scanner, run the script with the appropriate command-line arguments. Here's the basic usage:

```bash
python homology_scanner.py --reference <reference_file> --window <window_size> [other_arguments]
```

Replace `<reference_file>` with the path to the reference genome file, and `<window_size>` with the desired window size around the queried base to check homology.

For detailed information about the available command-line arguments and their usage, refer to the [Command-line Arguments](#command-line-arguments) section.

## Command-line Arguments

The Homology Scanner supports several command-line arguments to customize its behavior. Here are the available arguments:

- `-r, --reference <reference_file>`: Path to the reference genome file in FASTA format (required).
- `-w, --window <window_size>`: Window size around the queried base to check homology, specified in base pairs (default: 150).
- `-f, --input_file <input_file>`: Path to a tab-separated file with positions to check, one position per line (example: "1 1234"). If provided, the homology score will be calculated for all positions in the file.
- `-c, --chromosome <chromosome>`: Chromosome to check. Required when not using an input file.
- `-p, --position <position>`: Position to check. Required when not using an input file.
- `-b, --blat_output_prefix <output_prefix>`: Prefix for the output files generated by BLAT (default: "blat_output").
- `-o, --output_prefix <output_prefix>`: Prefix for the homology score output file (default: "homology_score_output").
- `-i, --fasta_index <fasta_index>`: Path to the FASTA index created with the fasta index creator function.
- `-I, --fasta_index_generator`: Generate a FASTA index for the chromosome specified by `-c`. This mode disables all other parameters.
- `-R, --read_generation_mode`: Generate reads at the queried position and introduce random mutations. Enabled only when both `-c` and `-p` arguments are provided.
- `-n_reads, --reads_number <reads_number>`: Number of reads to generate in read generation mode (default: 1000).
- `-BWA, --bwamem_index_generator_mode`: Generate the BWA-MEM index required for read generation mode. This mode disables all other parameters.
- `-bwa, --bwamem_index <bwamem_index>`: Path to the BWA-MEM index. Required for read generation mode.
- `-t, --treads <num_threads>`: Number of threads/CPUs available. This parameter affects only BWA-MEM (default: 4).
- `-m, --mutation_position <mutation_position>`: Relative position to mutate. Required when using read generation mode.
- `-a, --alternative <alternative>`: Base or bases to insert at the specified mutation position. Required when using read generation mode.

Note: Some command-line arguments may have additional requirements or dependencies. Refer to the script code or run `python homology_scanner.py --help` for detailed information.

## Examples

Here are a few examples demonstrating the usage of Homology Scanner:

1. Calculate the homology score for a specific position:

   ```bash
   python homology_scanner.py --reference genome.fasta --window 150 --chromosome 1 --position 1000
   ```

2. Generate reads at a specified position, introduce mutations, and calculate the homology score:

   ```bash
   python homology_scanner.py --reference genome.fasta --window 150 --chromosome 1 --position 1000 --read_generation_mode --mutation_position 10 --alternative A
   ```

3. Calculate the homology score for positions listed in an input file:

   ```bash
   python homology_scanner.py --reference genome.fasta --window 150 --input_file positions.txt
   ```

For more examples and information, please refer to the [Usage](#usage) section.

## Contributing

Contributions to the Homology Scanner are welcome! If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).
