# OpenPIV Skill

A Claude/Agent skill for Particle Image Velocimetry (PIV) analysis.

## What is OpenPIV?

OpenPIV is a powerful Python library for analyzing fluid flow from PIV image pairs. This skill provides:
- CLI for processing PIV image pairs
- Programmatic API for notebooks/scripts
- Velocity field extraction
- Vorticity computation
- Vector field visualization

## Installation

### Option 1: Using Skills CLI (Recommended)

```bash
npx skills add alexlib/openpiv-skill@openpiv
```

For global installation:
```bash
npx skills add alexlib/openpiv-skill@openpiv -g
```

### Option 2: Manual Installation

```bash
# Clone the repository
git clone https://github.com/alexlib/openpiv-skill.git

# Copy to your skills directory
cp -r openpiv-skill ~/.claude/skills/    # for Claude Code
# or
cp -r openpiv-skill ~/.agents/skills/    # for OpenCode
```

### Option 3: Install .skill Package

Download the `.skill` file from releases and install:
```bash
npx skills add /path/to/openpiv.skill
```

## Usage

### CLI

```bash
openpiv-process --image frame_a.bmp --image frame_b.bmp --output_dir results --verbose
```

### Python API

```python
from scripts import run_openpiv, PypivAnalyzer

# Run PIV analysis
run_openpiv("frame_a.bmp", "frame_b.bmp", verbose=True)

# Analyze results
analyzer = PypivAnalyzer("results/params.npz")
analyzer.plot_vector_field()

# Compute vorticity
vorticity = analyzer.compute_vorticity()
magnitude = analyzer.get_velocity_magnitude()
```

## Requirements

- Python 3.10+
- openpiv
- numpy
- matplotlib

Install dependencies:
```bash
uv pip install openpiv numpy matplotlib
```

## CLI Options

| Option | Default | Description |
|--------|---------|-------------|
| `--image` | required | Image file (specify twice for pair) |
| `--output_dir` | results | Output directory |
| `--algorithm` | openpiv_piv | PIV algorithm choice |
| `--mask` | none | Mask type: none, dynamic, static |
| `--window_size` | 32 | Interrogation window size (px) |
| `--overlap` | 12 | Window overlap (px) |
| `--dt` | 0.02 | Time between frames (s) |
| `--scaling` | 96.52 | Scaling factor (pixels/meter) |
| `--verbose` | False | Print progress messages |

## Output Files

- `vectors.txt` - Velocity vectors (x, y, u, v, flags)
- `params.npz` - NumPy archive with arrays
- `vector_field.png` - Visualization

## For Claude/Agent Users

This skill automatically triggers when you mention:
- PIV, particle image velocimetry
- Fluid flow analysis
- Velocity field extraction
- Vorticity computation
- Flow visualization

## License

See [LICENSE](LICENSE) - Apache 2.0

## Contributing

We welcome contributions! Please follow this workflow:

### 1. Fork the Repository

Click the "Fork" button on https://github.com/alexlib/openpiv-skill

### 2. Clone Your Fork

```bash
git clone https://github.com/YOUR_USERNAME/openpiv-skill.git
cd openpiv-skill
```

### 3. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
```

### 4. Make Your Changes

Edit the relevant files:
- `SKILL.md` - Skill documentation
- `scripts/` - Code (runner.py, analyze.py)
- `tests/` - Test cases
- `references/` - Additional docs

### 5. Test Your Changes

Run the test suite:
```bash
uv pip install -e .
uv run pytest tests/ -v
```

Test the CLI manually:
```bash
openpiv-process --image tutorials/sample_data/exp1_001_a.bmp --image tutorials/sample_data/exp1_001_b.bmp --output_dir test_output
```

### 6. Commit Your Changes

```bash
git add .
git commit -m "Add: description of your changes"
```

### 7. Push to Your Fork

```bash
git push origin feature/your-feature-name
```

### 8. Create a Pull Request

1. Go to https://github.com/alexlib/openpiv-skill
2. Click "Compare & pull request"
3. Describe your changes
4. Submit

### Contribution Guidelines

- Follow existing code style
- Add tests for new features
- Update documentation
- Be responsive to review feedback

## Resources

- [OpenPIV Python](https://github.com/openpiv/openpiv-python)
- [Skills CLI](https://skills.sh/)