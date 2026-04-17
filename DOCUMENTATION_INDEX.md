# bs-cpg Documentation Index

## 📖 Complete Documentation Structure

### Getting Started
- **[Installation](nbs/index.ipynb)** - Multiple installation methods and setup
- **[Quick Start](nbs/index.ipynb)** - 5-minute introduction with example code

---

## 📚 Module Documentation

### 1. **Setup & Configuration** [`01_setup.ipynb`](nbs/01_setup.ipynb)
   - Data path management
   - Configuration priority: Environment → Config File → User Prompt
   - Sample data access
   - **Key Functions:**
     - `get_base_data_path()` - Determine data storage location
     - `read_sample_cpg()` - Load sample CpG data for testing

### 2. **Data Acquisition** [`00_download_processed_geo.ipynb`](nbs/00_download_processed_geo.ipynb)
   - GEO (Gene Expression Omnibus) integration
   - Download processed RRBS data (BED format)
   - Resilient fetching with automatic retries
   - Local caching for efficiency
   - **Key Classes:**
     - `Geofetcher` - Enhanced GEO data fetcher with resilience

### 3. **Reference Management** [`02_download_ref.ipynb`](nbs/02_download_ref.ipynb)
   - Download reference genomes from UCSC
   - Automatic bgzip compression handling
   - Download liftover chain files
   - **Key Functions:**
     - `get_ref_genome()` - Download and prepare reference genomes
     - `get_liftover_chain()` - Download chain files for coordinate conversion
     - `is_bgzipped()` - Check compression format
     - `convert_to_bgzip()` - Convert standard gzip to bgzip
     - `download_file()` - General-purpose file downloader

### 4. **Coordinate Processing** [`03_liftover_pos.ipynb`](nbs/03_liftover_pos.ipynb)
   - Genomic liftover between genome builds
   - CpG site validation
   - Automatic genome and indexing detection
   - **Key Functions:**
     - `cpg_reads()` - Fetch 2-bp sequences from reference
     - `cpg_percent()` - Calculate percentage of valid CpG sites
     - `liftover_positions()` - Convert coordinates between builds
     - `guess_ref_and_index_base()` - Auto-detect genome build and indexing

---

## 👨‍💻 For Developers

### [Developer Guide](nbs/04_developers.ipynb)
- Project structure and organization
- Development environment setup
- nbdev workflow and directives
- How to add new functions
- Dependency management
- Publishing procedures
- Troubleshooting

---

## 🎓 Examples & Tutorials

### [Examples & Tutorials](nbs/05_examples.ipynb)
1. **Working with Sample Data** - Load and explore RRBS data
2. **Validating CpG Sites** - Verify positions contain valid CG dinucleotides
3. **Genomic Liftover** - Convert hg19 coordinates to hg38
4. **Genome Detection** - Auto-identify reference build and indexing
5. **Downloading References** - Fetch genomes and chain files
6. **Complete Pipeline** - End-to-end workflow example

Plus:
- Performance optimization tips
- Common pitfalls and solutions
- Working with your own data

---

## 🔄 Workflow Examples

### Basic Workflow
```python
from bs_cpg.setup import read_sample_cpg
from bs_cpg.liftover_ps import cpg_reads, cpg_percent, liftover_positions

# Load data
df = read_sample_cpg(["chromosome", "pos"])

# Validate
reads = cpg_reads(df["chromosome"], df["pos"], "hg19", index_base=1)
print(f"Valid CpG: {cpg_percent(reads):.1f}%")

# Liftover
new_chroms, new_pos = liftover_positions(
    chromosomes=df["chromosome"],
    positions=df["pos"],
    genome_from="hg19",
    genome_to="hg38"
)
```

### Download Reference
```python
from bs_cpg.download_ref import get_ref_genome, get_liftover_chain

ref_path = get_ref_genome("hg38")
chain_path = get_liftover_chain("hg19", "hg38")
```

---

## 📋 Function Reference by Module

### `bs_cpg.setup`
| Function | Purpose |
|----------|---------|
| `get_base_data_path()` | Get/set base data storage directory |
| `read_sample_cpg()` | Load sample CpG data for testing |

### `bs_cpg.download_processed`
| Class | Purpose |
|-------|---------|
| `Geofetcher` | Enhanced GEO data fetcher with retries & caching |

### `bs_cpg.download_ref`
| Function | Purpose |
|----------|---------|
| `get_ref_genome()` | Download & prepare reference genome |
| `get_liftover_chain()` | Download chain file for liftover |
| `is_bgzipped()` | Check if file is bgzip compressed |
| `convert_to_bgzip()` | Convert standard gzip to bgzip |
| `download_file()` | General-purpose file downloader |

### `bs_cpg.liftover_ps`
| Function | Purpose |
|----------|---------|
| `cpg_reads()` | Fetch 2-bp sequences at positions |
| `cpg_percent()` | Calculate % of valid CpG sites |
| `liftover_positions()` | Liftover coordinates between builds |
| `guess_ref_and_index_base()` | Auto-detect genome & indexing |

---

## 🔧 Development Workflow

### Setup
```bash
git clone https://github.com/magistak/bs-cpg.git
cd bs-cpg
pip install -e .
pip install nbdev jupyter
```

### Edit and Export
```bash
# Edit notebooks in nbs/
# Then export code and run tests
nbdev_prepare

# Preview documentation locally
nbdev_preview
```

### Publish
```bash
# Push to GitHub
git push

# Deploy documentation
nbdev_ghp_deploy
```

---

## 📞 Support & Resources

- **GitHub Issues**: [magistak/bs-cpg/issues](https://github.com/magistak/bs-cpg/issues)
- **Documentation**: [magistak.github.io/bs-cpg](https://magistak.github.io/bs-cpg/)
- **PyPI**: [pypi.org/project/bs-cpg](https://pypi.org/project/bs-cpg/)

---

## 📝 Quick Links

| Link | Purpose |
|------|---------|
| [index.ipynb](nbs/index.ipynb) | Main landing page & quick start |
| [01_setup.ipynb](nbs/01_setup.ipynb) | Configuration & data management |
| [00_download_processed_geo.ipynb](nbs/00_download_processed_geo.ipynb) | GEO data retrieval |
| [02_download_ref.ipynb](nbs/02_download_ref.ipynb) | Reference genome & chain files |
| [03_liftover_pos.ipynb](nbs/03_liftover_pos.ipynb) | Coordinate processing & liftover |
| [04_developers.ipynb](nbs/04_developers.ipynb) | Development guide |
| [05_examples.ipynb](nbs/05_examples.ipynb) | Practical examples & tutorials |

---

## 📄 Document Information

- **Documentation Version**: Complete (April 2026)
- **Last Updated**: April 14, 2026
- **Format**: nbdev-based Jupyter Notebooks
- **Total Notebooks**: 7 comprehensive guides
- **Coverage**: 100% of public API functions

---

**Ready to get started? Begin with the [Quick Start](nbs/index.ipynb)!**
