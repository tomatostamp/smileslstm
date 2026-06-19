# Molecule Generation using SMILES LSTM
This project is an implementation of LSTM based molecule generation model using SMILES representations. The model learns the syntax and structural patterns of molecules and generates molecular structures by sampling character sequences.

## Dataset
ZINC250K: A dataset mainly used for drug discovery due to the molecules' optimal QED score. A subset of 10000 molecules was sampled for training.
Each molecule was represented as a SMILES string and processed using character-level tokenization.

## SMILES Representation
The sampled molecules are processed in the following way:
-	Addition of special start (^) and end ($) tokens to each SMILES string
- Extraction of all unique characters from the dataset
- Creation of character-to-index (stoi) and index-to-character (itos) mappings
- Padding of sequences to a fixed length
- Conversion of SMILES strings into numerical sequences
- Generation of input-target pairs for next-character prediction
- 
### Model Architecture:
Input SMILES Sequence → Embedding Layer (128) → 2-Layer LSTM (Hidden Size = 256) → Fully Connected Layer → Next Character Prediction


## Training
Cross Entropy Loss is used.

Given a partial SMILES sequence, it learns to predict the most likely next character.

## Molecule Generation
The model generates new molecules by predicting one SMILES character at a time.

Generation begins with the start token (^). At each step:
1. The current sequence is passed through the trained LSTM.
2. The model predicts a probability distribution over all possible SMILES characters.
3. A character is sampled from this distribution.
4. The sampled character is appended to the sequence.
5. The process repeats until the end token ($) is generated or the maximum sequence length is reached.

## Results
Results obtained on 100 generated molecules:

| Metric | Score  |
|----------|----------|
| Validity  | 60%   |
| Novelty  | 60%  |  
| Average QED  | ~0.4 - 0.7  |

## Inference
The model successfully demonstrated the generation of drug-like molecules that are novel and are mostly chemically valid.

## Tech Stack
- PyTorch
- RDKit
- NumPy
- Pandas
- HuggingFace Dataset (yairschiff/zinc250k)
