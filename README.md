# Contribution [1]: Add More Rust API Examples

**Contribution Number:** [1]  
**Student:** [Nathan Bezabeh]  
**Issue:** [[GitHub issue link](https://github.com/k2-fsa/sherpa-onnx/tree/master/rust-api-examples)]  
**Status:** [Phase IV/In progress]

---

## Why I Chose This Issue

[I chose this issue because it connects well with my goals in software engineering and AI. The sherpa-onnx project is related to speech recognition and machine learning tooling, which makes it more interesting and useful for my background than a basic documentation-only issue. The issue asks for more Rust API examples, and the repository already has existing C API examples and Rust examples that I can use as references.

This issue also fits the project timeline because I can narrow the scope to one specific example instead of trying to complete the entire issue. My goal is to work on one missing Rust API example, such as a non-streaming Paraformer example, and follow the structure already used in the repository. I chose it because it will help me practice reading an open-source codebase, learning Rust patterns, testing code locally, and submitting a clean pull request.]

---

## Understanding the Issue

### Problem Description

The sherpa-onnx repository has C API examples for Paraformer, but the Rust API examples folder does not currently have a matching Paraformer Rust example. This makes it harder for Rust users to understand how to run a Paraformer ASR model using the Rust API.

### Expected Behavior

The rust-api-examples/examples folder should include a Rust example that shows how to run a Paraformer ASR model, similar to how the C API folder already includes Paraformer examples.

### Current Behavior

The C API folder includes Paraformer examples, but the Rust examples folder does not show a matching Paraformer example when I search for it locally.

### Affected Components

The main affected areas are:
- rust-api-examples/examples
- rust-api-examples/README.md
- possible helper script in rust-api-examples
- c-api-examples/paraformer-c-api.c as the reference example

---
## Reproduction Process

### Environment Setup

I cloned my fork of the k2-fsa/sherpa-onnx repository and opened it locally in VS Code on Windows. I navigated into the rust-api-examples folder and tried to run the basic Rust example.

At first, I ran into a setup issue where PowerShell returned cargo is not recognized. This meant Rust/Cargo was not installed or was not available in my PATH. I fixed this by installing Rust with rustup, reopening VS Code, and confirming that Cargo was working.

### After setup, I ran:

cargo run --example version

The command successfully compiled and ran the Rust example. The output showed:

Version : 1.13.3
Git SHA1: 330609da
Git date: Mon Jun 15 07:50:54 2026
Steps to Reproduce
Clone my fork of the repository.
Navigate into the Rust API examples folder:
cd sherpa-onnx/rust-api-examples
Confirm the Rust example environment works:
cargo run --example version
Check whether Paraformer C API examples exist:
dir ..\c-api-examples\*paraformer*
The C API examples folder includes Paraformer reference files, including paraformer-c-api.c and streaming-paraformer-c-api.c.
Check whether a matching Rust Paraformer example exists:
dir .\examples\*paraformer*
No matching Rust Paraformer example appears in the rust-api-examples/examples folder.

### Reproduction Evidence

Branch showing reproduction: [add-rust-paraformer-example](https://github.com/nati2405/sherpa-onnx/tree/add-rust-paraformer-example)
Screenshots/logs: Local terminal output showed cargo run --example version working successfully.
My findings: The C API has Paraformer examples, but the Rust API examples folder does not currently include a matching Paraformer Rust example.

### Solution Approach

### Analysis

The issue appears to be a missing example rather than a broken runtime feature. The project already has C API examples for Paraformer and several existing Rust API examples for other models. The root problem is that Rust users do not currently have a Paraformer example to follow in the Rust examples folder.

### Proposed Solution

I plan to add a new Rust API example for non-streaming Paraformer by using the existing C API Paraformer example as a reference and matching the style of the existing Rust examples.

### Implementation Plan

Using UMPIRE framework:

### Understand:
The problem is that sherpa-onnx has Paraformer examples for the C API, but not a matching example for the Rust API.

### Match:
I will compare c-api-examples/paraformer-c-api.c with similar Rust examples inside rust-api-examples/examples to understand how the Rust examples handle model configuration, input audio, recognition, and output.

### Plan:

Review c-api-examples/paraformer-c-api.c.
Review existing Rust ASR examples in rust-api-examples/examples.
Create a new Rust example file for non-streaming Paraformer.
Follow the same structure and naming style used by the existing Rust examples.
Add or update a helper script if the repository expects one.
Run the new example locally.
Run an existing example again to make sure the current setup still works.

### Implement:
Implementation will happen in Phase III on this branch:
add-rust-paraformer-example

### Review:
I will compare my example against the existing Rust examples to make sure the code style, file naming, and command structure are consistent with the project.

### Evaluate:
I will verify the solution by running the new Paraformer Rust example locally. I will also run cargo run --example version again to confirm the Rust examples still compile correctly.

## Testing Strategy

### Unit Tests

- [x] Confirmed the new Rust example compiles by running `cargo check --example paraformer`.
- [x] Confirmed the existing Rust example setup still works by running `cargo run --example version`.
- [x] Confirmed the new Paraformer Rust example accepts model, tokens, and WAV file arguments correctly.

### Integration Tests

- [x] Downloaded and extracted the Paraformer model package locally.
- [x] Ran the new Paraformer Rust example end-to-end with `test_wavs/0.wav`.
- [x] Confirmed the example produced decoded text and a performance summary.

### Manual Testing

I manually tested the new Rust example by running:

### Implementation Notes

Week 1 Progress

Completed Phase I by selecting the sherpa-onnx Rust API examples issue, narrowing the scope to one missing Rust example, and writing why I chose the issue.

Week 2 Progress

Completed Phase II setup and reproduction. I cloned my fork locally, created the working branch, installed Rust/Cargo, verified that the Rust examples compile by running cargo run --example version, confirmed that Paraformer C API examples exist, and confirmed that a matching Rust Paraformer example is currently missing.

Week 3 Progress

Started Phase III implementation. I added a new Rust example file for non-streaming Paraformer and created a helper script to download the model and run the example. I tested the example locally with the Paraformer model and confirmed it runs successfully end-to-end.

Week 4 Progress

Completed Phase IV by opening a pull request to the upstream `k2-fsa/sherpa-onnx` repository. The PR is currently awaiting maintainer review.

## Code Changes:

Files modified: 
  - rust-api-examples/examples/paraformer.rs
  - rust-api-examples/run-paraformer.sh

Key commits:
  - Add Paraformer Rust API example
  - Add Paraformer Rust example script
    
Approach decisions: I followed the structure of existing Rust ASR examples and used c-api-examples/paraformer-c-api.c as the main reference for model paths, tokens, WAV input, and offline recognizer behavior.
---

## Pull Request

**PR Link:** [[GitHub PR URL when submitted](https://github.com/k2-fsa/sherpa-onnx/pull/3707)]

**PR Description:** 

I submitted a pull request to the upstream k2-fsa/sherpa-onnx repository that adds a non-streaming Paraformer example for the Rust API. The PR adds a new Rust example file and a helper run script so Rust users can run Paraformer ASR using a model file, tokens file, and WAV input.

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review]

---

## Learnings & Reflections

### Technical Skills Gained

I learned how to work inside a Rust example project, create a new Rust API example, run `cargo check`, pass command-line arguments with `clap`, and test an offline speech recognition model locally.

### Challenges Overcome

The biggest challenge was setting up Rust/Cargo on Windows and making sure the Paraformer model files were downloaded correctly. I first ran into a `cargo is not recognized` issue, then later had to manually download and extract the Paraformer model before the example could run end-to-end.

### What I'd Do Differently Next Time

Next time, I would check the existing run scripts and model download steps earlier before testing the example. That would make it easier to know whether a failure is from my code or just from missing model/audio files.

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
