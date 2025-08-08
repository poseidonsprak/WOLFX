[wolf x] - Agentless Vulnerability Scanner 

Chapter 1: Introduction
1.1 Background
With increasing reliance on distributed IT/OT infrastructure, modern organizations face expanding attack surfaces. Traditional agent-based vulnerability scanners introduce overhead and can be incompatible with air-gapped or sensitive environments. A SaaS-based, agentless solution is needed to ensure continuous visibility into security risks across networks without intrusive deployment requirements.
1.2 Purpose of the System
The platform aims to deliver a comprehensive, scalable, agentless vulnerability scanning service via a SaaS model. It supports scanning across Windows, Linux, and OT systems without deploying agents. It also offers advanced features like passive discovery, AI-driven risk prioritization, integrations with external tools, and a rich dashboard for real-time threat visualization.
1.3 Advantages
No agent deployment required


Passive and active scanning supported


Prioritizes risks using EPSS and AI


Provides intuitive dashboards for security teams


Supports OT/IT environments in a unified interface


Chapter 2: System Analysis
2.1 Problem Statement
Traditional vulnerability scanners are not well-suited for diverse environments with operational and legacy systems. They often require intrusive agent installation, leading to performance degradation, compliance issues, or operational risks, especially in sensitive OT environments.
2.2 Feasibility Study
By leveraging secure remote protocols (SSH, WMI), passive sniffing (PCAP, Zeek), and open vulnerability databases (NVD, EPSS, ExploitDB), a cloud-hosted scanning engine in Python can deliver cross-platform vulnerability management. The system is feasible using scalable microservices for task scheduling, result processing, and AI-based analytics.
2.3 Operational Efficiency
The system allows fast, non-intrusive scanning across various networks. Cloud-based orchestration with scheduling ensures scans can run automatically or on demand. Intelligent risk scoring and integrations reduce the need for manual triage, making the process more efficient and less error-prone.
Chapter 3: Module Description
3.1 Central Controller (Node.js Backend)
Handles user authentication, scheduling, scanner job queuing, integration with tools (Jira, Slack), and management of results and reports. Orchestrates communication between frontend, scanner, and database systems.
3.2 Scanning Modules (Python Engine)
Linux/Windows Scanner: Uses SSH or WinRM to pull package/service info and perform vulnerability matching.


OT Scanner: Uses Modbus, BACnet simulation and PCAP parsing to identify legacy vulnerabilities.


Passive Discovery: Leverages Zeek/Nmap to monitor network activity and fingerprint assets.


3.3 AI Risk Prioritization
A lightweight AI module processes CVSS, EPSS, asset sensitivity, and exploit availability to prioritize scan results. It uses LLM-based models (e.g., OpenAI or local LLaMA) to suggest remediation.
3.4 Reporting and Dashboard (React Frontend)
Real-time dashboard mimics VulsRepo with additions like CVE filtering, graphical heatmaps, scan histories, asset risk charts, and exportable compliance reports (CSV, PDF).
Chapter 4: System Design


4.1 Architectural Design
Frontend: React + Tailwind for UI


Backend: Node.js + Express for APIs and task orchestration


Scanner: Python microservice for executing actual scan logic


Database: PostgreSQL (assets, users, vulnerabilities), Redis (job queues), and Elasticsearch (log analytics)



4.2 UI/UX Design
Clean, intuitive web interface with role-based access. Supports themes, user preferences, and multi-tenant environments. The dashboard offers real-time updates, clickable drill-downs, and reporting features.
4.3 Security Design
JWT-based authentication


RBAC (Admin, Analyst, Viewer roles)


HTTPS encrypted communication


Secure credential vault for SSH/WinRM keys


No persistent access to scanned systems


Chapter 5: System Development
5.1 Development Methodology
Agile sprint-based development with weekly milestones. Core modules (scan engine, risk scoring, backend API, dashboard) were developed incrementally and tested in staging environments.
5.2 Tools and Technologies
Frontend: React.js, TailwindCSS, Axios


Backend: Node.js, Express, PostgreSQL, Redis, BullMQ


Scanner: Python 3, Paramiko, Nmap, Zeek, pywinrm, pymodbus


AI: OpenAI API / Ollama


Logging: Elasticsearch + Logstash


DevOps: Docker, Docker Compose, GitHub Actions


5.3 Database Development
PostgreSQL used for asset/user/scan data. Redis used for queuing scan jobs. Elasticsearch indexes log events and scanner outputs.

Chapter 6: System Testing
6.1 Unit and Integration Testing
Each module (frontend/backend/scanner) includes unit tests.


Integration tested with real Linux and Windows hosts.


Webhooks tested for Jira and Slack.


6.2 Functional Testing
Scans run successfully across Linux, Windows, and OT testbeds.


Users assigned roles and verified RBAC enforcement.


AI-based risk outputs matched expected CVSS/EPSS weightings.


6.3 Performance and Load Testing
Redis-based queues handled parallel scan jobs under load.


Frontend remained responsive with thousands of CVE entries.


Scanner performance scaled using containers and horizontal scaling.



Chapter 7: Implementation
7.1 Deployment Setup
The platform is deployed on AWS with Docker-based microservices. Services are distributed via Kubernetes with autoscaling. Secrets are managed via AWS Secrets Manager.
7.2 Installation Steps
Deploy PostgreSQL, Redis, Elasticsearch using docker-compose


Deploy scanner and backend services


Connect frontend to backend APIs


Configure initial admin account and upload SSH/WinRM keys


Run scheduled or manual scans


7.3 Maintenance and Updates
CVE/NVD/EPSS feeds updated nightly


Scanner modules support plugin-based expansion


Webhooks and integrations are modular and can be extended



Chapter 8: Conclusion
8.1 Summary of Achievements
The project delivers a cloud-hosted, agentless vulnerability scanner supporting Windows, Linux, and OT systems. It includes AI-based prioritization, integrations with enterprise tools, and user-friendly dashboards with compliance reporting.
8.2 Benefits to Organizations
No need to install agents on critical systems


Unified visibility across IT and OT assets


Faster time-to-remediation via AI-based suggestions


Seamless integration with existing security ecosystems


8.3 Future Enhancements
Full offline scan support (air-gapped factory environments)


Integration with SIEM and SOAR platforms


Automated remediation via scripting


Threat intelligence feed ingestion (e.g., MISP, AlienVault OTX)



Chapter 9: References
Python Official Documentation


Node.js Official Documentation


React.js Official Docs


Nmap Network Scanning Guide


Zeek Network Security Monitor


EPSS by FIRST


ExploitDB


OpenAI API Docs


Cybersecurity Frameworks (NIST, ISO)
