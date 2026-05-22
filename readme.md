# CIE Engineered Controls

A research repository from the **Cyber-Informed Engineering (CIE)** program at Idaho National Laboratory. This repository contains the Engineered Controls Database — a catalog of physical and procedural controls mapped to cyber-physical resilience roles across all 18 DHS Critical Infrastructure sectors — along with a browser-based dashboard for exploring it.

---

## What Is Cyber-Informed Engineering?

Cyber-Informed Engineering (CIE) is a methodology developed at Idaho National Laboratory that integrates cybersecurity thinking directly into the engineering design and operation of critical infrastructure. Rather than treating cyber threats as a purely IT concern, CIE embeds security considerations into physical system design so that engineered safeguards provide resilience even when digital controls are compromised or manipulated.

More information: [inl.gov/cie](https://inl.gov/cie)

---

## Repository Structure

```cmd
/
├── GUI/        Browser-based dashboard for exploring the controls database
└── Data/       Engineered Controls Database and supporting data files
```

### GUI

The `GUI/` directory contains a standalone HTML dashboard — **CIE Engineered Controls Explorer** — that runs entirely in the browser with no installation required. Load your data files and explore controls by sector hierarchy, filter by resilience role or control type, search across all entries, and view analytics. See `GUI/README.md` for usage instructions.

### Data

The `Data/` directory contains the Engineered Controls Database JSON file and the IDF Infrastructure Taxonomy file used to power the hierarchy browser. See `Data/README.md` for file format documentation.

---

## Authors

**Benjamin Lampe**
Idaho National Laboratory — Cyber-Informed Engineering Program
<benjamin.lampe@inl.gov>
