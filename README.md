---
# PROBLEM STATEMENT
---

ContractNLI is a dataset for document-level natural language inference (NLI) on contracts whose goal is to automate/support a time-consuming procedure of contract review. In this task, a system is given a set of hypotheses (such as "Some obligations of Agreement may survive termination.") and a contract, and it is asked to classify whether each hypothesis is entailed by, contradicting to or not mentioned by (neutral to) the contract

![img](https://stanfordnlp.github.io/contract-nli/resources/task_overview.png)

## Dataset specification
We have 17 hypotheses annotated on 607 non-disclosure agreements (NDAs). The hypotheses are fixed throughout all the contracts including the test dataset.

- The task is Natural language inference (NLI): Document-level three-class classification (one of Entailment, Contradiction or NotMentioned).

**The core information in our dataset is:**

- `text`: The full document text
- `spans`: List of spans as pairs of the start and end character indices.
- `annotation_sets`: It is provided as a list to accommodate multiple annotations per document.
- `annotations`: Each key represents a hypothesis key. choice is either Entailment, Contradiction or NotMentioned. **`spans`** is given as indices of spans above. spans is empty when choice is NotMentioned.
- `labels`: Each key represents a hypothesis key. hypothesis is the hypothesis text that should be used in NLI.


**Our dataset is provided as JSON files.**

```json
{
  "documents": [
    {
      "id": 1,
      "file_name": "example.pdf",
      "text": "NON-DISCLOSURE AGREEMENT\nThis NON-DISCLOSURE AGREEMENT (\"Agreement\") is entered into this ...",
      "document_type": "search-pdf",
      "url": "https://examplecontract.com/example.pdf",
      "spans": [
        [0, 24],
        [25, 89],
        ...
      ],
      "annotation_sets": [
        {
          "annotations": {
            "nda-1": {
              "choice": "Entailment",
              "spans": [
                12,
                13,
                91
              ]
            },
            "nda-2": {
              "choice": "NotMentioned",
              "spans": []
            },
            ...
          }
        }
      ]
    },
    ...
  ],
  "labels": {
    "nda-1": {
      "short_description": "Explicit identification",
      "hypothesis": "All Confidential Information shall be expressly identified by the Disclosing Party."
    },
    ...
  }
}
```

