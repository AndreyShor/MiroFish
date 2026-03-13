# MiroFish API Reference

The MiroFish backend is a Flask-based REST API that orchestrates the GraphRAG construction and OASIS simulation workflow.

---

## 📂 Blueprints

The API is divided into three main blueprints:
1. `graph_bp`: Project and Knowledge Graph management.
2. `simulation_bp`: Simulation lifecycle and agent interaction.
3. `report_bp`: Analytics and prediction reporting.

---

## 🧠 Graph API (`/api/graph`)

### Project Management
- **GET** `/list`: List all projects.
- **GET** `/<project_id>`: Get detailed information about a specific project.
- **DELETE** `/<project_id>`: Delete a project and its associated data.
- **POST** `/reset/<project_id>`: Reset project state to rebuild the graph.

### Graph Construction
- **POST** `/ontology`: Upload files (PDT, MD, TXT) and trigger LLM-based ontology generation.
- **POST** `/build`: Start the asynchronous graph building task in Zep Cloud.
- **GET** `/task/<task_id>`: Query the status of an ongoing graph build task.

### Data Access
- **GET** `/data/<graph_id>`: Retrieve all nodes and edges for D3.js visualization.
- **DELETE** `/<graph_id>`: Delete the knowledge graph from Zep Cloud.

---

## 🎮 Simulation API (`/api/simulation`)

### Lifecycle Management
- **POST** `/create`: Initialize a new simulation for a project.
- **POST** `/prepare`: Start an async task to generate agent personas and configurations.
- **GET** `/prepare/status`: Check the progress of the preparation task.
- **POST** `/run`: Launch the parallel OASIS simulation (Twitter/Reddit).
- **POST** `/stop`: Terminate running simulation processes.

### Monitoring & Interaction
- **GET** `/<simulation_id>`: Get current simulation status and round progress.
- **GET** `/history`: List historical simulations with project metadata.
- **GET** `/profiles/<simulation_id>`: Retrieve generated agent personas.
- **POST** `/interview`: Conduct a real-time interview with a running agent.

---

## 📊 Report API (`/api/report`)

### Generation
- **POST** `/generate`: Trigger the Report Agent to analyze simulation results.
- **GET** `/generate/status`: Monitor report generation progress.

### Retrieval
- **GET** `/list`: List all generated reports.
- **GET** `/<report_id>`: Retrieve report metadata and full Markdown content.
- **GET** `/simulation/<simulation_id>`: Get the report associated with a specific simulation.
- **GET** `/download/<report_id>`: Download the report as a `.md` file.

### Interactive Analysis
- **POST** `/chat`: Chat with the Report Agent about the simulation results. Uses ReACT logic to retrieve facts from the graph.

---

## 🛠 Common Response Formats

### Success
```json
{
  "success": true,
  "data": { ... }
}
```

### Error
```json
{
  "success": false,
  "error": "Error message description",
  "traceback": "..." (only in debug mode)
}
```
