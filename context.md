Below is a consolidated, confidentiality-safe session context for your portfolio website. Company and client names have been replaced with industry descriptions.

# Portfolio Profile Context

## Professional Positioning

**Senior Data Scientist specializing in Generative AI, agentic systems, mathematical optimization and production machine learning.**

Four years of experience designing and delivering AI systems for procurement, energy, petrochemicals, manufacturing and industrial research. Work includes multi-agent platforms, retrieval-augmented generation, private LLM deployments, model fine-tuning, real-time optimization, production scheduling, AutoML and MLOps.

Responsibilities have included:

* Solution architecture and technical design
* Project planning and delivery leadership
* Backend and AI-system development
* Mathematical modelling and optimization
* LLM evaluation, observability and guardrails
* Scalable deployment on Kubernetes
* Mentoring and technical interviewing
* Productization of client-specific solutions
* Collaboration with domain experts, engineering teams and business stakeholders

---

# Featured Projects

## 1. Intelligent Procurement and Vendor-Collaboration Platform

### Overview

Designed the architecture for an enterprise procurement platform that uses multiple AI agents to automate RFQ tracking, vendor communication, compliance checks, purchase-order fulfilment and procurement-related queries.

The platform consolidated information distributed across enterprise procurement systems, email, transactional databases and uploaded documents into a role-aware dashboard and conversational interface.

### Business problem

Procurement teams had to manually track large numbers of RFQs, technical bids, commercial bids, purchase orders, delivery milestones and vendor documents across disconnected systems.

Buyers spent significant time:

* Following up with vendors
* Sending reminders and escalations
* Tracking procurement stages
* Checking whether required documents had been submitted
* Responding to repetitive vendor questions
* Reconstructing information from email and enterprise systems
* Coordinating with plant users and internal stakeholders

Vendors also lacked a single interface for understanding submission requirements, delivery locations, deadlines and procurement status.

### Solution

Designed a multi-agent workflow consisting of five specialized agents and a supervisor agent.

#### Supervisor Agent

* Identified the current procurement stage
* Routed tasks to the appropriate specialized agent
* Controlled workflow transitions
* Prevented invalid stage changes
* Ensured that commercial, technical and post-PO activities were handled in the correct order

#### Quotation and RFQ Agent

* Tracked RFQs across procurement systems, databases and email
* Monitored document-submission status
* Sent reminders to vendors
* Escalated delayed submissions
* Helped buyers understand the current state of each RFQ

#### Fulfilment Agent

* Tracked post-purchase-order activities
* Monitored delivery and contractual milestones
* Generated reminders and escalation messages
* Helped buyers identify delayed or at-risk purchase orders

#### Query Agent

* Answered vendor, buyer and plant-user questions
* Supported both chatbot and email-based interactions
* Retrieved information from structured databases and unstructured documents
* Generated contextual responses according to the user’s role

#### Compliance and Guardrail Agent

* Validated user queries
* Detected out-of-scope or unsafe requests
* Prevented sensitive information from being exposed
* Verified generated responses before they were returned to users

#### Audit and Traceability Components

* Recorded agent actions and routing decisions
* Captured retrieval and generation traces
* Supported debugging and compliance reviews

### Agentic RAG architecture

The platform used a layered retrieval strategy designed to reduce latency and LLM cost.

1. A small language model classified the user’s intent.
2. Simple factual questions were routed to SQL queries.
3. Frequently requested information was returned through predefined response templates.
4. Complex questions triggered document retrieval.
5. Relevant context was retrieved using hybrid search.
6. A large language model generated the response from the retrieved evidence.
7. Retrieval quality and answer quality were evaluated.
8. A confidence score was calculated using retrieval similarity and LLM-based evaluation.
9. Low-confidence responses were withheld or converted into clarification requests.
10. Final responses passed through guardrails before reaching the user.

The system avoided hallucinating missing information. When the request was ambiguous, the agent asked a follow-up question. When structured data was unavailable, the system moved to document-based retrieval rather than inventing an answer.

### Security and access control

* Implemented role-based access for vendors, buyers and plant users
* Restricted users to the RFQs, purchase orders and documents assigned to them
* Added checks for prompt injection, data leakage and irrelevant queries
* Validated both incoming requests and outgoing responses
* Maintained traceability for agent decisions and generated answers

### Scalability

Designed asynchronous processing for approximately **2,000 concurrent users** using:

* RabbitMQ
* Celery
* Redis
* Kubernetes
* KEDA

KEDA dynamically scaled the application based on workload and queue activity.

### Technologies

LangGraph, Python, agentic RAG, hybrid retrieval, SQL, Elasticsearch vector search, Gemini, small language models, NeMo Guardrails, Langfuse, RabbitMQ, Celery, Redis, Kubernetes and KEDA.

### Contribution

* Designed the overall solution architecture
* Planned the agent responsibilities and orchestration
* Defined retrieval, routing and confidence-scoring logic
* Designed security and guardrail workflows
* Contributed to scalability and deployment planning
* Participated in project planning and technical leadership

---

## 2. CataLLM: AI-Assisted Catalyst Research Engine

### Overview

Led the development of an AI research platform that analyzed more than **50,000 patents and technical documents** to assist researchers with catalyst discovery.

The system identified technically relevant documents, created a curated research corpus and used a fine-tuned language model to generate evidence-backed research hypotheses.

### Business problem

Catalyst researchers had to manually review large volumes of patents and technical literature before proposing new formulations.

This process was slow because:

* Relevant information was buried in long chemical documents
* Keyword search generated large numbers of false positives
* Many documents were only partially relevant
* Sending every document to an LLM would be expensive
* General-purpose LLMs lacked sufficient domain adaptation
* Researchers needed outputs grounded in curated evidence

The larger objective was to reduce catalyst R&D time while supporting improvements in catalyst life and process yield.

### Document-ingestion workflow

* Collected and parsed chemical patents and PDF documents
* Extracted usable text and metadata
* Normalized content for search and scoring
* Applied domain-specific keywords supplied by subject-matter experts
* Stored the curated information for downstream retrieval and model training

### Two-stage relevance filtering

A staged filtering pipeline was created to balance precision and cost.

#### Stage 1: BM25 filtering

BM25 was used as an inexpensive first-pass retrieval method.

Documents below the configured BM25 threshold were removed before LLM evaluation.

#### Stage 2: LLM relevance scoring

Only documents that passed the BM25 threshold were sent to the LLM.

The model evaluated whether each document was relevant to the research objectives and client-defined technical criteria.

Documents had to satisfy both lexical and semantic thresholds before entering the final research corpus.

This approach reduced unnecessary LLM calls and improved the quality of the training and retrieval dataset.

### Model fine-tuning

A Gemma model was fine-tuned using **QLoRA** on the curated research corpus.

The fine-tuned model generated:

* Catalyst-related research hypotheses
* Potential formulations
* Evidence-backed technical observations
* Research directions
* Structured summaries of relevant technical findings

### Results

* Processed more than **50,000 patents and documents**
* Achieved approximately **65% relevance** in the selected research corpus
* Reduced irrelevant documents through combined BM25 and LLM scoring
* Deployed the solution on Google Cloud
* Created a reusable document-intelligence workflow for technical R&D

### Technologies

Python, Gemma, QLoRA, BM25, LLM-based relevance scoring, document parsing, PDF processing, retrieval systems and Google Cloud.

### Contribution

* Led the technical development
* Designed the multi-stage document-filtering strategy
* Defined the interaction between BM25 and LLM scoring
* Contributed to dataset curation
* Led the model fine-tuning approach
* Supported deployment and delivery

---

## 3. Real-Time Optimization for Petrochemical Operations

### Overview

Developed a real-time optimization system for a naphtha-cracker operation to improve ethylene and propylene production while maximizing operating margin.

The system operated under real plant constraints, including coking-related limitations, equipment restrictions and reduced operating flexibility.

### Business problem

Petrochemical plants must continuously adjust operating variables to improve yield and margin. However, the search space is highly constrained and simulator evaluations can be computationally expensive.

The optimizer had to:

* Maximize product yield
* Improve operating margin
* Respect plant and equipment constraints
* Work with process-simulator outputs
* Generate feasible recommendations
* Operate quickly enough for practical plant use

### Optimization approach

Implemented a Differential Evolution-based optimizer using the **JADE algorithm**.

The solution included:

* Objective-function configuration
* Decision-variable bounds
* Constraint handling
* Process-simulator integration
* Feasibility checks
* Parallel evaluation
* Result ranking and recommendation generation

### Performance improvement

Optimization candidates were evaluated in parallel using multiprocessing.

This reduced optimization runtime by approximately **90%**, enabling substantially faster search across the operating space.

### Reported operational impact

During constrained plant operation, the system achieved client-reported improvements of approximately:

* **1.5%–1.8% yield maximization**
* **₹3,000–₹4,000 per ton-hour margin improvement**

### Productization

The original implementation was developed for a specific operating environment. The next phase focused on converting the solution into a reusable product for other refineries and petrochemical plants.

The productization work involved:

* Separating plant-specific logic from the optimization engine
* Designing configurable objectives and constraints
* Supporting different simulator and data interfaces
* Standardizing deployment and monitoring
* Creating reusable optimization components

Future enhancements explored the use of machine learning or an LLM-guided component to generate better initial vectors. The objective was to begin optimization from more promising regions of the search space and reduce convergence time.

### Technologies

Python, JADE, Differential Evolution, multiprocessing, constrained optimization, process simulation and industrial data integration.

### Contribution

* Developed the optimization engine
* Integrated the optimizer with the process simulator
* Improved runtime through multiprocessing
* Created reusable optimization components
* Led the productization initiative
* Explored ML-assisted initialization strategies

---

## 4. Grade Market and Sequence Optimization

### Overview

Developed optimization systems for grade allocation, production sequencing and market assignment in polymer-manufacturing operations.

The solution supported plants producing grades such as HDPE, PP and LLDPE.

### Business problem

Production planners needed to decide:

* Which grades to manufacture
* In what sequence the grades should run
* Which market or customer should receive each grade
* How contractual commitments should be satisfied
* How changeover costs and production restrictions should be handled
* How total contribution margin could be maximized

Manual planning was difficult because production, inventory, demand, customer commitments and operational constraints interacted with one another.

### Solution

Built a mixed-integer optimization model covering:

* Grade-to-market allocation
* Production sequencing
* Contract adherence
* Demand fulfilment
* Capacity restrictions
* Changeover logic
* Plant-specific operating constraints
* Margin maximization

The broader solution included two connected capabilities.

#### Grade Market Assigner

Determined the best market or customer allocation for available production while respecting demand and contractual commitments.

#### Grade Sequence Optimizer

Generated a feasible production sequence that reduced operational inefficiency while meeting commercial requirements.

### Impact

The scheduling and allocation solution delivered approximately **₹2 crore in profit or business benefit** through improved production and market decisions.

### Technologies

Python, mixed-integer linear programming, Gurobi, CPLEX, PuLP, scheduling optimization and constraint modelling.

### Contribution

* Designed the optimization formulation
* Converted business rules into mathematical constraints
* Developed market-allocation and sequence-optimization logic
* Worked with domain experts to validate feasibility
* Supported implementation and delivery

---

## 5. Global and Location-Specific Drilling Fluid Models

### Overview

Developed machine-learning models for predicting drilling-fluid rheology and thickening time across more than **one million records** from over **50 global locations**.

The complete solution was delivered in less than two months.

### Business problem

Model performance varied across locations because:

* Some locations had large datasets
* Some had limited historical observations
* Geological and operational patterns differed
* A single global model did not always perform best
* Small local datasets created overfitting and reliability risks

The project required a systematic way to determine when to use global models, local models or grouped-location models.

### Modelling strategy

Built and compared:

* Global models trained on all locations
* Local models trained for individual locations
* Grouped-location models combining similar or data-sparse locations

XGBoost was selected as the primary modelling algorithm.

The workflow included:

* Data cleaning and validation
* Feature engineering
* Stratified sampling
* Location-aware dataset splitting
* Time-dependent modelling logic
* Rule-based preprocessing
* Model comparison
* Error analysis
* Automated accuracy tracking

### Challenges addressed

* Uneven data availability across locations
* Location-specific operating behaviour
* Complex domain rules
* Time-dependent patterns
* Model-selection logic at the location level
* Automated performance comparison

### Results

* Scaled modelling across **1M+ records**
* Supported **50+ locations**
* Delivered global, local and grouped model comparisons
* Completed delivery in under two months
* Created automated pipelines for model training and accuracy monitoring

### Technologies

Python, Pandas, NumPy, scikit-learn, XGBoost, time-series modelling, stratified sampling and automated ML pipelines.

### Contribution

* Designed the modelling strategy
* Developed global and local model comparisons
* Implemented feature and rule-based logic
* Created automated training and evaluation pipelines
* Supported delivery under an aggressive timeline

---

## 6. Private LLM-Based Technical Proposal Generation

### Overview

Developed a private LLM application that generated structured technical proposals from requests for proposal, reference documents and historical proposal examples.

The system was designed for an engineering organization operating in a data-sensitive industrial domain.

### Business problem

Engineers spent substantial time manually preparing technical proposals.

Each proposal required:

* Reading long request documents
* Identifying technical requirements
* Reusing relevant historical language
* Maintaining section-level consistency
* Adapting content to the new opportunity
* Preserving confidential information

The objective was to reduce repetitive proposal-writing effort so that engineers could focus on technical and commercial analysis.

### Solution

Implemented a section-wise generation workflow.

Instead of generating the complete proposal in one step, each section was handled independently.

For example:

* The introduction used examples of previous introductions
* The technical approach used examples of comparable technical sections
* Scope and assumptions used their corresponding historical examples
* Each section received the relevant input and expected output format

This few-shot strategy improved structure and consistency.

### Private model deployment

A Llama 3.1 model was self-hosted and served through vLLM.

This architecture was selected to:

* Keep confidential documents within the organization’s environment
* Avoid external API exposure
* Support controlled inference
* Improve throughput through efficient model serving

### Technologies

Python, Llama 3.1, vLLM, few-shot prompting, PDF parsing, document intelligence and private LLM deployment.

### Contribution

* Designed the section-wise generation workflow
* Defined few-shot examples and prompt structures
* Integrated proposal and request documents
* Supported self-hosted inference architecture
* Contributed to privacy and security design

---

## 7. Reusable Data Science CI/CD and MLOps Framework

### Overview

Helped standardize the deployment process for data-science services by designing an automated CI/CD framework in collaboration with the DevSecOps team.

The framework supported model validation, code-quality checks, security scanning and API deployment.

### Business problem

Data-science projects followed inconsistent deployment processes.

Common gaps included:

* Manual validation
* Inconsistent testing
* Missing security checks
* Limited model-regression protection
* Different API structures across projects
* High dependency on individual developers
* Lack of standardized deployment gates

### Automated pipeline

The Jenkins-based workflow included:

* Code linting
* Bandit security scanning
* Pytest unit tests
* Golden-dataset model checks
* Existing-versus-new-model comparison
* Threshold-based pipeline failure
* Automated FastAPI or Flask service deployment

A model was not deployed when its performance failed the configured threshold against the golden dataset.

The process was designed to require minimal human involvement. Once a deployment request was initiated, the pipeline ran the configured checks and deployed the service only after all quality gates passed.

### Future direction

The framework was planned to support:

* Agent evaluation
* Agentic application deployment
* Prompt and workflow regression testing
* LLM observability
* Agent performance monitoring
* Safety and guardrail checks

### Technologies

Jenkins, Python, FastAPI, Flask, pytest, Bandit, linting, model validation, Docker, Kubernetes, MLflow, Airflow and Kubeflow.

### Contribution

* Worked with DevSecOps to define the delivery workflow
* Implemented data-science-specific quality gates
* Designed golden-dataset validation
* Standardized API deployment
* Mentored teams on CI/CD practices

---

## 8. Reusable AutoML Framework

### Overview

Developed a reusable AutoML framework for an industrial analytics platform.

The framework allowed teams to create complete machine-learning pipelines without repeatedly implementing the same feature-engineering, model-selection and evaluation components.

### Capabilities

* Dataset validation
* Feature engineering
* Train-test preparation
* Model selection
* Hyperparameter optimization
* Model training
* Error-metric generation
* Model comparison
* Result reporting

The framework allowed users to choose between internal logic and existing AutoML libraries such as:

* TPOT
* PyCaret
* AutoGluon

### Objective

The framework reduced repeated development effort and provided a consistent way to compare models across different industrial projects.

### Technologies

Python, scikit-learn, TPOT, PyCaret, AutoGluon, Pandas and automated evaluation pipelines.

### Contribution

* Designed the reusable framework
* Integrated multiple AutoML libraries
* Implemented feature-engineering and evaluation stages
* Supported integration into an industrial analytics platform
* Led a team involved in its development

---

## 9. Reusable JADE Optimization Framework

### Overview

Created a configurable optimization framework based on the JADE variant of Differential Evolution.

The framework allowed teams to apply the optimizer to new problems by defining:

* Objective functions
* Decision variables
* Variable bounds
* Constraints
* Feasibility conditions
* Evaluation logic

### Value

The framework separated problem-specific logic from the underlying optimization algorithm.

This reduced the effort required to implement new industrial optimization use cases and enabled consistent experimentation across projects.

### Technologies

Python, Differential Evolution, JADE, constraint handling and multiprocessing.

### Contribution

* Designed the reusable architecture
* Implemented the optimization engine
* Standardized objective and constraint interfaces
* Improved evaluation speed through parallel processing

---

## 10. Yarn Production Scheduling Optimizer

### Overview

Developed a rule-based and mathematical scheduling system for a textile manufacturer.

The solution assigned yarn-production requirements to machines and production lines while respecting operational constraints.

### Business problem

Production planners had to coordinate:

* Yarn types
* Fabric requirements
* Machine compatibility
* Production-line availability
* Sequence restrictions
* Capacity limits
* Client-defined production rules

### Solution

Developed:

* A mixed-integer scheduling optimizer
* A rule-based scheduling engine
* Constraint-validation logic
* Machine and production-line assignment workflows

### Contribution

* Led a team of three
* Converted operational rules into scheduling logic
* Designed the optimization model
* Supported validation with domain stakeholders

### Technologies

Python, MILP, scheduling optimization, Gurobi, CPLEX and rule-based systems.

---

## 11. Industrial Process Simulator Integration

### Overview

Developed an end-to-end integration between Python and an industrial process simulator.

The connector allowed optimization and analytics applications to programmatically:

* Send operating parameters
* Trigger simulator runs
* Retrieve output values
* Validate results
* Use simulator responses inside optimization loops

### Value

The integration enabled automated evaluation of candidate operating conditions and removed the need for repeated manual simulator interaction.

### Technologies

Python, process simulation, industrial-system integration and optimization workflows.

---

## 12. Engineering Spreadsheet Connector and Parser

### Overview

Developed and deployed a parser that extracted engineering inputs from spreadsheet-based workflows and calculated required process parameters.

The solution supported calculations related to ethylene, propylene and other operational variables.

### Capabilities

* Spreadsheet ingestion
* Input validation
* Parameter extraction
* Calculation logic
* Structured output generation
* Integration with downstream optimization workflows

### Value

The connector reduced manual data-entry effort and standardized the flow of engineering inputs into analytical applications.

---

## 13. Greenfield Petrochemical Plant Design Optimizer

### Overview

Developed a design-stage optimizer to evaluate the feasibility of establishing a new petrochemical plant.

### Business problem

Plant-design decisions required balancing:

* Production targets
* Process configurations
* Capital and operating constraints
* Feedstock assumptions
* Product mix
* Equipment limitations
* Economic feasibility

### Solution

Developed an optimization workflow that evaluated candidate plant configurations against technical and commercial constraints.

### Contribution

* Defined the optimization structure
* Implemented feasibility checks
* Integrated engineering calculations
* Generated comparative design scenarios

---

## 14. Reinforcement Learning Portfolio Management Prototype

### Overview

Developed an experimental stock-portfolio management solution using Q-learning.

### Objective

The project explored whether an agent could learn portfolio-allocation decisions from market states and reward signals.

### Components

* Market-state definition
* Action-space design
* Reward-function formulation
* Q-learning implementation
* Portfolio-value tracking
* Strategy evaluation

### Positioning note

This is better presented as an earlier experimentation project rather than a flagship portfolio project because it is less relevant than the production GenAI and optimization systems.

---

# Independent Project

## 15. Agentic Applicant Tracking and Recruitment Platform

### Overview

Architected and developed the backend of a deployed recruitment platform designed to reduce the time and manual effort required to move candidates through the hiring process.

The product supports:

* Candidates
* HR teams
* Hiring managers
* Business-unit leaders
* Interviewers and reviewers

### Business problem

Hiring teams often use disconnected systems for:

* Creating job descriptions
* Screening resumes
* Generating interview questions
* Tracking candidate progress
* Recording decisions
* Maintaining audit trails
* Coordinating stakeholders

The objective was to combine these workflows into one agentic platform.

### Agent architecture

The platform contains six agents and supporting automations.

#### Job Description Agent

* Helps create structured job descriptions
* Converts hiring requirements into role-specific content
* Standardizes job-description formatting

#### Resume Screening Agent

* Evaluates candidate resumes against job requirements
* Produces structured screening observations
* Supports candidate prioritization

#### Interview Question Generator

* Creates role-specific interview questions
* Adapts questions to experience level and skill requirements
* Supports structured technical evaluation

#### Traceability Agent

* Records workflow events
* Tracks important decisions
* Maintains visibility across the hiring process

#### Audit Agent

* Reviews system actions
* Supports accountability and process checks
* Helps identify missing or inconsistent workflow information

#### Workflow Automation Agent

* Coordinates repetitive hiring activities
* Moves information between stages
* Reduces manual follow-up effort

### Product design

The system includes:

* A candidate-facing portal
* An HR and hiring-manager portal
* Role-aware workflows
* Agent orchestration
* Self-hosted model inference
* Audit and traceability functionality

### Private model deployment

A quantized Gemma 2B model is self-hosted through Ollama.

This provides:

* Local inference
* Improved data privacy
* Lower dependency on third-party APIs
* Greater control over model configuration

### Current status

The platform is deployed and functional.

Ongoing improvements focus on:

* Latency reduction
* Error handling
* Resilience
* Evaluation
* Monitoring
* Production readiness
* Enterprise-grade security
* Workflow reliability

### Technologies

LangGraph, Python, Gemma 2B, Ollama, React and AI-assisted frontend development.

### Contribution

* Designed the overall architecture
* Developed the backend
* Implemented agent workflows
* Integrated the self-hosted model
* Defined product and hiring workflows
* Used AI-assisted coding for frontend development

### Repository

`github.com/kogantisasank831-ux/rms-app-optimized`

---

# Leadership and Organizational Contributions

## Agentic AI Innovation Guild

* Leads an internal innovation group focused on agentic systems
* Explores reusable agent architectures
* Supports knowledge-sharing across projects
* Evaluates frameworks and implementation patterns
* Helps teams understand practical applications of agents and LLMs

## DevOps and Optimization Guilds

* Co-leads initiatives related to optimization and DevOps
* Contributes reusable technical patterns
* Supports standardization across projects
* Helps teams adopt better engineering and deployment practices

## Mentoring

* Mentored approximately five to six team members
* Guided team members on Git workflows
* Supported Kubernetes adoption
* Helped developers understand optimization and production AI practices

## Hiring

* Interviewed approximately 10–12 candidates for Generative AI engineering roles
* Evaluated candidates on LLM concepts, agentic systems, backend development and practical problem-solving

## Team Leadership

* Managed or directly led two team members
* Led larger project teams of up to five members
* Supported architecture, task planning and technical reviews

---

# Recognition

* Promoted to Senior Consultant in July 2025 while working in a Senior Data Scientist capacity
* Received an individual Spot Award
* Received a Team Spot Award for real-time optimization delivery

---

# Core Technical Skills

## Generative AI and Agentic Systems

LangGraph, agentic RAG, multi-agent orchestration, supervisor-agent patterns, QLoRA, few-shot prompting, prompt design, LLM-as-judge evaluation, confidence scoring, NeMo Guardrails and agent traceability.

## Models and Inference

Gemma, Llama 3.1, Gemini, quantized models, Ollama, vLLM and self-hosted inference.

## Retrieval and Search

BM25, hybrid retrieval, semantic search, SQL-first routing, Elasticsearch vector search, cosine similarity and document-ranking pipelines.

## Machine Learning

Python, Pandas, NumPy, scikit-learn, XGBoost, time-series modelling, feature engineering, model selection, AutoML and error analysis.

## Optimization

Differential Evolution, JADE, MILP, scheduling, sequence optimization, Gurobi, CPLEX, PuLP, constraint modelling and multiprocessing.

## Backend Engineering

Python, FastAPI, Flask, SQL, PostgreSQL, MariaDB, REST APIs and asynchronous processing.

## Infrastructure

Docker, Kubernetes, KEDA, RabbitMQ, Celery, Redis and Google Cloud.

## MLOps and Observability

Jenkins, MLflow, Airflow, Kubeflow, Langfuse, pytest, Bandit, linting, golden-dataset testing and automated deployment pipelines.

---

# Recommended Portfolio Categories

For the website, the projects should be divided into four categories.

## Generative AI and Agentic Systems

* Intelligent Procurement Platform
* CataLLM
* Private Proposal Generation
* Agentic Applicant Tracking Platform

## Machine Learning

* Global and Local Drilling Fluid Models\
* Reusable AutoML Framework
* Reinforcement Learning Portfolio Prototype

## Mathematical Optimization

* Real-Time Petrochemical Optimization
* Grade Market and Sequence Optimization
* Yarn Scheduling Optimizer
* JADE Optimization Framework
* Greenfield Plant Design Optimizer

## AI Engineering and MLOps

* Data Science CI/CD Framework
* Industrial Simulator Integration
* Spreadsheet Connector and Parser

For the homepage, the strongest featured projects are:

1. Intelligent Procurement and Vendor-Collaboration Platform
2. CataLLM Research Engine
3. Real-Time Petrochemical Optimization
4. Grade Market and Sequence Optimization
5. Agentic Applicant Tracking Platform
6. Global Drilling Fluid Prediction Platform
