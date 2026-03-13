# MiroFish GraphRAG Guide

MiroFish uses **GraphRAG (Retrieval-Augmented Generation)** to create a structured and queryable memory of the world being simulated. This is powered by **Zep Cloud**.

---

## 🏗 The Graph Construction Process

The knowledge graph is built in two primary stages:

### 1. Ontology Generation
Before building the graph, the system must define the "schema" of the world.
- **Service**: `OntologyGenerator`
- **Logic**: Analyzes uploaded documents using an LLM to identify:
    - **Entity Types**: e.g., Person, Organization, Concept, Event.
    - **Relationship Types**: e.g., "MEMBER_OF", "WORKS_AT", "INFLUENCES".
- **Outcome**: A JSON definition that guides the subsequent graph construction.

### 2. Graph Building
Once the ontology is set, the raw text is processed into a formal graph.
- **Service**: `GraphBuilderService`
- **Logic**:
    - **Chunking**: Splits source text into manageable pieces using semantic-aware splitting.
    - **Extraction**: Uses LLM-based extraction to find entities and relations defined in the ontology.
    - **Persistence**: Data is sent to **Zep Cloud** in batches, where it is indexed and linked.
- **Outcome**: A persistent, queryable knowledge network in Zep Cloud.

---

## 🧠 Role in Simulations

The knowledge graph serves three critical functions:

1. **Persona Grounding**: When generating agent personas, the `OasisProfileGenerator` queries the graph to ensure agent backgrounds and motivations are factually consistent with the seed documentation.
2. **Contextual Retrieval**: During simulation, agents can "recall" facts or relationships from the graph to inform their social interactions.
3. **Report Intelligence**: The `ReportAgent` uses the graph to perform complex reasoning, such as "Identify all organizations influenced by Person X" or "Trace the evolution of Concept Y across the simulation".

---

## ⚡ Zep Cloud Integration

MiroFish uses Zep Cloud for state-of-the-art graph memory management:
- **Scalability**: Handles large-scale graphs with thousands of entities.
- **Fast Retrieval**: Optimized for relationship-based queries (sub-graph extraction).
- **Persistence**: Allows for "snapshots" of the world state, enabling users to restart or branch simulations from specific points in the story.

---

## 📊 Visualizing the Graph

Users can explore the knowledge network in real-time through the MiroFish UI, which uses **D3.js** to render:
- **Nodes**: Representing entities, color-coded by type.
- **Edges**: Representing relationships, with directional links and labels.
- **Details**: Clicking any node or edge reveals the raw text excerpts (chunks) from which it was extracted.
