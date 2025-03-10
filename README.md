# masdel-antivirus
College Project

------------------------------------------------------------

# AI-Powered Antivirus System Project Plan

**Objective:**  
Develop an antivirus system with two main components:
1. **Local Antivirus Application**  
   - Written in **Rust** for high-performance file scanning, network monitoring, and firewall control.
   - Uses **Python** for an AI malware classifier.
   - Integration via either **PyO3** (embedding Python in Rust) or a REST-based microservice (using Flask).
2. **Cloud-Hosted Web Dashboard**  
   - Built with **Django** and **Django REST Framework**.
   - Uses **PostgreSQL** for data storage.
   - Provides secure, real-time visualizations of scan logs and threat alerts.

**Overall Data Flow:**  
1. The Rust app scans files and monitors network traffic.  
2. File data is passed to the Python AI module for classification.  
3. Combined scan results (file and network data) are transmitted securely to the Django REST API.  
4. The Django web dashboard displays logs, alerts, and reports.

---

## Table of Contents

- [Week 1: Planning, Environment Setup & Initial Research](#week-1-planning-environment-setup--initial-research)
- [Week 2: Develop Local Antivirus File Scanner in Rust](#week-2-develop-local-antivirus-file-scanner-in-rust)
- [Week 3: Enhance Scanner with Multi-threading & Network Monitoring](#week-3-enhance-scanner-with-multi-threading--network-monitoring)
- [Week 4: Build the Python AI Malware Classifier](#week-4-build-the-python-ai-malware-classifier)
- [Week 5: Integrate Rust Scanner with Python AI Module](#week-5-integrate-rust-scanner-with-python-ai-module)
- [Week 6: Build Django REST API & Web Dashboard](#week-6-build-django-rest-api--web-dashboard)
- [Week 7: End-to-End Integration & Testing](#week-7-end-to-end-integration--testing)
- [Week 8: Final Optimization, Deployment & Documentation](#week-8-final-optimization-deployment--documentation)
- [Key Technologies & Libraries](#key-technologies--libraries)
- [Flow Diagram](#flow-diagram)
- [Best Practices Summary](#best-practices-summary)

---

## Week 1: Planning, Environment Setup & Initial Research

### Tasks & Technologies:
- **Project Scope & Documentation:**
  - Define clear objectives, deliverables, and milestones.
  - **Tools:** Markdown for documentation; [draw.io](https://app.diagrams.net) for architecture diagrams.

- **Version Control:**
  - Initialize a Git repository (GitHub or GitLab).
  - Establish a branching strategy (e.g., separate feature branches for Rust, Python, and Django modules).

- **Environment Setup:**
  - **Rust:**
    - Install via [Rustup](https://rustup.rs).
    - Familiarize with Cargo, rustfmt, and Clippy.
  - **Python:**
    - Create a virtual environment (using `venv` or `conda`).
    - Install libraries: TensorFlow or scikit-learn, NumPy, Pandas.
    - Optionally install [PyO3](https://pyo3.rs/) if using direct integration.
  - **Django:**
    - Install Django and Django REST Framework.
    - Set up PostgreSQL (locally for development; later on, use your chosen cloud provider).
  - **IDE/Editors:**  
    - Visual Studio Code, IntelliJ IDEA (with Rust plugin), or PyCharm.

### Security Measures

- **Rust & Python Security:**
  - Use **Clippy & RustSec** to catch vulnerabilities in Rust.
  - Use **Bandit** for Python static code analysis.

- **Django API Security:**
  - Implement **JWT or OAuth2** authentication.
  - Enforce **rate limiting** with Django REST Framework.
  - Enable **HTTPS** in production.

- **AWS Security:**
  - Secure PostgreSQL with **IAM roles & VPC**.
  - Use **AWS WAF & Shield** for DDoS protection.
  - Store secrets in **AWS Secrets Manager** instead of `.env` files.

### Expected Features

- **Real-time Threat Detection:**
  - Web dashboard updates dynamically with scan logs.
  - Optional **email alerts** for high-risk detections.

- **Multi-threaded File Scanning:**
  - Rust scanner optimized with **Rayon** for performance.

- **Cloud-Based Scan Logs & Reports:**
  - Store past scans in **PostgreSQL** with **CSV/JSON export** options.

- **User Roles & Permissions:**
  - Implement **Admin vs. Standard User** access control.

- **REST API for Remote Scanning:**
  - Enable external clients to submit files for scanning via API.

### Debugging & Logging Strategy

- **Rust Logging (File Scanner & Network Monitoring)**
  - Uses `log` and `env_logger` crates.
  - Can be enabled/disabled via environment variables.

- **Python AI Module Logging**
  - Uses built-in `logging` module with log levels (`INFO`, `WARNING`, `ERROR`).
  - Easily toggle logging via config.

- **Django API Logging**
  - Uses Django's built-in logging system.
  - Logs can be stored locally or in AWS CloudWatch.

- **Optional Sentry Integration**
  - Can capture and report errors across Rust, Python, and Django.
  - Completely removable if not needed.

### Milestones:
- Environment installation completed.
- Documented high-level architecture diagram:
  [Local System] -> [Rust Scanner] -> [Python AI Model] -> [Django API (Cloud)] -> [Web Dashboard]

## Week 1: Completed Tasks  

- ✅ Set up and activated Python virtual environment (`venv`).  
- ✅ Installed required Python libraries (`numpy`, `pandas`, `tensorflow`, `django`, etc.).  
- ✅ Installed Rust and verified setup (`rustc`, `cargo`).  
- ✅ Set up PostgreSQL, created `antivirus_db`, and connected it to Django.  
- ✅ Created and ran a simple Rust program (`hello.rs`).  
- ✅ Implemented basic logging (`debug_logger.py`) and verified `antivirus.log`.  

---

## Week 2: Develop Local Antivirus File Scanner in Rust

### Modules & Technologies:
- **File Traversal Module:**
- **Technology:** Rust, Cargo, `std::fs`, and the [`walkdir`](https://crates.io/crates/walkdir) crate.
- **Tasks:**
  - Write functions to recursively scan directories and list files.
  - Use proper error handling with Rust’s `Result` type.
  - Write unit tests using Rust’s test framework.

- **File Content Analysis Module:**
- **Technology:** Rust, optional [`yara-rust`](https://crates.io/crates/yara) crate.
- **Tasks:**
  - Develop functions to read file content.
  - Compare file content against malware signatures (simulate or use YARA rules).
  - Log scan results locally using the [`log`](https://crates.io/crates/log) crate.

### Milestones:
- File traversal and content scanning modules are implemented.
- Unit tests passing with sample data.

---

## Week 3: Enhance Scanner with Multi-threading & Network Monitoring

### Modules & Technologies:
- **Performance Optimization:**
- **Technology:** Use the [Rayon](https://crates.io/crates/rayon) crate for parallel processing.
- **Tasks:**
  - Refactor file scanning to run concurrently.
  - Benchmark using `cargo bench` and profile with Rust tools.

- **Network Monitoring Module:**
- **Technology:** Rust, [`pcap`](https://crates.io/crates/pcap) crate.
- **Tasks:**
  - Write functions to capture packets from the network interface.
  - Analyze packet headers to detect suspicious patterns (e.g., port scans).
  - Log network events with timestamps.

### Milestones:
- Multi-threaded file scanning is operational.
- Basic network packet capture and logging functionality is in place.

---

## Week 4: Build the Python AI Malware Classifier

### Modules & Technologies:
- **Data Preparation & Model Training:**
- **Technology:** Python, scikit-learn or TensorFlow/Keras, Pandas, NumPy.
- **Tasks:**
  - Gather and preprocess sample datasets (malware vs. benign).
  - Select and train a lightweight model (e.g., Random Forest, SVM, or a small neural network).
  - Validate and evaluate model performance.
  - Save the model (using `pickle` or TensorFlow SavedModel).

- **Inference Module:**
- **Technology:** Python.
- **Tasks:**
  - Write a function to load the model and perform inference on file data.
  - Write unit tests for the inference function.

### Milestones:
- AI model is trained, validated, and saved.
- Inference function is working and tested.

---

## Week 5: Integrate Rust Scanner with Python AI Module

### Integration Options & Technologies:
- **Option 1 – Using PyO3 (Direct Integration):**
- **Technology:** [PyO3](https://pyo3.rs/).
- **Tasks:**
  - Create Rust bindings to call the Python inference function.
  - Serialize data appropriately (JSON or native types via PyO3).
  - Implement error handling for integration.

- **Option 2 – Using a REST API (Microservice Approach):**
- **Technology:** Flask for Python REST API, Rust HTTP client with [`reqwest`](https://crates.io/crates/reqwest).
- **Tasks:**
  - Develop a minimal Flask app exposing a `/predict` endpoint.
  - Write Rust client code to send HTTP requests with file data in JSON.
  - Parse and log the response.

### Milestones:
- Choose and implement an integration method.
- Successfully retrieve classification results from the Python AI module in Rust.
- Document integration details and data formats.

---

## Week 6: Build Django REST API & Web Dashboard

### Modules & Technologies:
- **Django REST API:**
- **Technology:** Django, Django REST Framework, PostgreSQL.
- **Tasks:**
  - Create a new Django project.
  - Define models (e.g., `ScanLog`, `ThreatAlert`, `User`).
  - Develop secure REST API endpoints for receiving scan results and logs.
  - Secure endpoints with JWT or API keys.
  - Write tests (using Django's test framework or Postman).

- **Web Dashboard:**
- **Technology:** Django Templates, Bootstrap 4/5.
- **Tasks:**
  - Build a user-friendly dashboard to display scan logs, alerts, and reports.
  - Implement views and templates with responsive design.
  - Optionally, add AJAX or Django Channels for real-time updates.

### Milestones:
- Django API endpoints are operational and secured.
- Web dashboard displays data correctly.
- Cloud deployment configuration (e.g., on Heroku, AWS, or DigitalOcean) is set up for Django.

---

## Week 7: End-to-End Integration & Testing

### Tasks & Technologies:
- **System Integration:**
- **Technology:** Secure data transfer via HTTPS; optionally, use WebSockets for real-time data.
- **Tasks:**
  - Integrate the local antivirus modules (Rust and Python) with the Django API.
  - Package the scan results into JSON and send them securely.
  - Validate that data is correctly stored in PostgreSQL via the Django API.

- **End-to-End Testing:**
- **Tasks:**
  - Simulate full workflows: file scan → AI inference → data push → dashboard update.
  - Use automated tests and manual testing (e.g., Postman, browser testing).
  - Conduct security tests (input validation, authentication).

### Milestones:
- Full integration from local scanning to the web dashboard is complete.
- Document issues and fixes found during testing.

---

## Week 8: Final Optimization, Deployment & Documentation

### Tasks & Technologies:
- **Optimization:**
- **Rust:** Profile using `cargo bench`, optimize multi-threading and asynchronous operations (consider [Tokio](https://tokio.rs/) if needed).
- **Python:** Fine-tune the AI model if necessary.
- **Django:** Optimize API endpoints (consider async views in Django 3.1+).
- **Deployment:**
- **Local App:** Package Rust executable and Python scripts; prepare an installation guide.
- **Django App:** Deploy to a cloud provider (Heroku, AWS Elastic Beanstalk, or DigitalOcean). Configure SSL, environment variables, and domain names.
- **Documentation & Presentation:**
- **Final Report:**  
  - Introduction & Objectives.
  - Detailed System Architecture & Data Flow Diagrams.
  - Module Descriptions: Rust Scanner, Python AI Module, Django API & Dashboard.
  - Testing Results, Performance Metrics, and Security Audits.
  - User Manual & Deployment Instructions.
- **Presentation:** Prepare slides summarizing the project design, challenges, and outcomes.

### Milestones:
- Optimized and fully deployed system.
- Final documentation and presentation are complete.

---

## Key Technologies & Libraries

- **Rust:**
- **Language & Tools:** Rust, Cargo.
- **Crates:** `std::fs`, `walkdir`, `rayon`, `pcap`, `yara-rust`, `reqwest`, `tokio` (if async needed), [PyO3](https://pyo3.rs/).
- **Python:**
- **Language & Environment:** Python 3.x, virtualenv/conda.
- **Libraries:** TensorFlow or scikit-learn, Pandas, NumPy, pickle; Flask (if using REST API); PyO3 (if direct integration).
- **Django:**
- **Framework:** Django, Django REST Framework.
- **Database:** PostgreSQL.
- **Frontend:** Django Templates, Bootstrap 4/5.
- **Deployment & Tools:**
- **Cloud Hosting for Django:** Heroku, AWS Elastic Beanstalk, or DigitalOcean.
- **Version Control:** Git (GitHub/GitLab).
- **Documentation:** Markdown, GitHub Wiki, or ReadTheDocs.
- **Testing:** Rust unit tests, Python unittest/pytest, Django test framework, Postman.

---

## Flow Diagram

[Local System: User Files & Network Traffic]
         │
         ▼
[Rust Scanner Module]
 ├── File Traversal (std::fs, walkdir)
 ├── File Content Scan (YARA, yara-rust)
 └── Network Monitoring (pcap)
         │
         ▼
[Python AI Module]
 ├── Data Preprocessing (Pandas, NumPy)
 ├── Model Training (scikit-learn/TensorFlow)
 └── Inference (pickle/TensorFlow SavedModel)
         │
         ▼
[Integration Layer]
 ├── PyO3 bindings  
 └── Flask REST API (called via reqwest in Rust)
         │
         ▼
[Django REST API (Cloud)]
 ├── API Endpoints (Django REST Framework)
 └── PostgreSQL Database
         │
         ▼
[Web Dashboard]
 ├── Django Templates & Bootstrap
 └── Real-time Data (AJAX / Django Channels)


---

## Best Practices Summary

- **Version Control:**  
  - Commit frequently; use branching for major features.
- **Modularity:**  
  - Develop and test modules separately before integration.
- **Documentation:**  
  - Maintain clear, updated documentation and inline code comments.
- **Security:**  
  - Validate all inputs; secure API endpoints.
- **Testing:**  
  - Write unit tests and integration tests for every module.
- **Performance:**  
  - Profile code and optimize with multi-threading and async operations.
- **CI/CD:**  
  - If possible, set up continuous integration for automated testing (e.g., GitHub Actions).

---

This document provides a comprehensive, detailed, and technology-specific roadmap for building your AI-powered antivirus system over the next two months. It covers everything from planning and environment setup to module development, integration, testing, and deployment.

*Feel free to add more details or adjust the timeline based on your progress and learning curve.*

---

*End of Project Plan*

