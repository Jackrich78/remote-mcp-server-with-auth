Project Constitution: Secure, Multi-Client MCP Server
This document provides the master context for our project. It defines the mission, architecture, principles, and execution plan. As the project's AI assistant, you must adhere to the information and principles outlined here at all times.

1. Core Mission & Objective
Our primary objective is to build, test, and deploy a secure, production-ready MCP (Model Context Protocol) server. This project is a hands-on learning exercise focused on best practices for local development, robust security (authentication & authorization), and scalable cloud deployment.

The final artifact will be a secure database tool server accessible from multiple AI clients, primarily TypingMind and the Gemini CLI.

2. Guiding Principles
These are the non-negotiable rules for our development process:

Security First: All steps must prioritize security. This includes handling secrets correctly (never in source code), implementing authentication (GitHub OAuth), and validating inputs. DO NOT ask for or display the values of secrets. Refer to them only by their variable names (e.g., DATABASE_URL).
Environment Parity: To minimize deployment issues, our local development environment must mirror the production environment as closely as possible. We will use a cloud-hosted PostgreSQL database (Neon) for both local and production work.
Reproducibility & Isolation: The environment must be reproducible. We will use nvm to manage the Node.js version on a per-project basis. We will not use a local Postgres installation.
Clean Directory Structure: The workspace is organized into distinct, single-responsibility sub-projects. All work should be contained within the appropriate sub-directory.
3. Technology Stack
Language: TypeScript
Runtime: Node.js (version managed by nvm)
Deployment Platform: Cloudflare Workers
CLI Tooling: Cloudflare Wrangler, Gemini CLI
Database: PostgreSQL (hosted on Neon)
Authentication: GitHub OAuth
Primary Clients: TypingMind (Desktop App), Gemini CLI
4. Project Architecture & Directory Structure
This is a multi-project workspace. The root directory contains isolated sub-projects for each phase.

cloudflare-mcps/
├── secure-db-server/         # Phase 2 & 3: The main secure database server project.
│   ├── .dev.vars             # Local development secrets (read by `wrangler dev`).
│   ├── wrangler.toml         # Cloudflare configuration file.
│   └── ...                   # Cloned from coleam00/remote-mcp-server-with-auth.
│
└── gemini.md                 # This file: our project's master context.
5. Phased Execution Plan (Our Roadmap)
We are following a "Crawl, Walk, Run" approach.

Phase 1 (Crawl): Implement the sequential-thinking MCP server. The goal is to get a simple, local server running and connected to TypingMind to validate the basic MCP client-server loop.
Phase 2 (Walk): Implement the secure-db-server locally. This involves configuring GitHub OAuth, connecting to our Neon database, and testing the secure tools from TypingMind and the Gemini CLI.
Phase 3 (Run): Deploy the secure-db-server to Cloudflare Workers. This involves configuring production secrets, updating GitHub callback URLs, and testing the live, public endpoint.
6. Key Configuration & Secrets Reference
The following environment variables are required across our projects.

For sequential-thinking (in .env file):

OPENAI_API_KEY
For secure-db-server (in .dev.vars for local, Cloudflare secrets for prod):

DATABASE_URL (Points to our Neon DB)
GITHUB_CLIENT_ID
GITHUB_CLIENT_SECRET
ENCRYPTION_KEY
7. Useful Links & Resources
Sequential Thinking Repo: https://github.com/typingmind/sequential-thinking-mcp
Secure DB Server Repo: https://github.com/coleam00/remote-mcp-server-with-auth
TypingMind MCP Docs: https://docs.typingmind.com/model-context-protocol-(mcp)-in-typingmind
Neon Database: https://neon.tech
Cloudflare Dashboard: https://dash.cloudflare.com
GitHub OAuth Apps: https://github.com/settings/developers