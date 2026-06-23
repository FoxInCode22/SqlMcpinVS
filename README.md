  # Exploring SQL MCP Server with Azure SQL & Data API Builder in VS Code

With SQL MCP Server now Generally Available, I wanted to validate its capabilities and explore how it enables secure AI-to-database interactions in a real-world environment.   

As AI-powered development tools such as GitHub Copilot become integral to engineering workflows, organizations need a governed approach for exposing enterprise data to AI agents. Allowing an LLM to generate arbitrary SQL introduces security, compliance, and operational risks. While natural language access to databases is compelling, enterprise architects must ensure that access remains auditable, secure, and aligned with existing governance controls.    

SQL MCP Server addresses this challenge by exposing approved database entities and operations as Model Context Protocol (MCP) tools. AI agents can discover and invoke these tools through controlled schemas and permissions rather than issuing unrestricted SQL statements directly against a database.  

Being a database architect, I was particularly interested in understanding whether SQL MCP Server could provide a secure alternative to traditional NL2SQL approaches. My goal was to evaluate the setup experience, governance model, and how effectively GitHub Copilot could interact with relational data exposed through MCP.

  Built into Data API Builder (DAB), SQL MCP Server supports:    
  	• Azure SQL Database    
  	• SQL Server    
  	• PostgreSQL    
  	• MySQL    
  	• Azure Cosmos DB    
  
By leveraging DAB, MCP endpoints inherit existing capabilities such as authentication, role-based access control (RBAC), telemetry, and API governance, providing a secure integration layer between AI agents and enterprise data sources.
In this walkthrough, I used an existing Azure SQL Database hosting the AdventureWorksLT sample database and evaluated how quickly I could expose the data through REST, GraphQL, and MCP endpoints for consumption by AI-powered tools such as GitHub Copilot.


## What is Data API Builder (DAB)?
Data API Builder (DAB) is an open-source data gateway that automatically generates secure REST, GraphQL, and MCP endpoints directly from database objects with minimal configuration.
Rather than building and maintaining custom APIs, developers can expose tables, views, and stored procedures as secure endpoints through a simple configuration file.
DAB provides a unified access layer across multiple database platforms while enforcing centralized authentication, authorization, and data access policies.
With the introduction of SQL MCP Server, DAB extends beyond traditional API generation and enables databases to be exposed as MCP-compliant tools that can be safely consumed by AI agents such as GitHub Copilot.

  
## Architecture
  
<img width="368" height="224" alt="image" src="https://github.com/user-attachments/assets/3ee05400-c586-4511-a82d-05f02873f4f0" />

The SQL MCP Server acts as an abstraction layer between AI agents and the database, exposing approved entities through a deterministic contract instead of direct SQL access.

## Prerequisites
	
	Install the following software:
	
	Component	                          Version
	.NET SDK	                          8.0 or later
	Visual Studio Code	                  Latest
	GitHub Copilot Extension	          Latest
	SQL Server Management Studio (SSMS)	  Latest
	Azure SQL Database	                  Any tier
	Data API Builder	                    1.7+
	SQL MCP Server support was introduced in Data API Builder 1.7 and continues in newer releases.

## Walkthrough

The setup and configuration process is already well covered in the official documentation. For this exercise, I focused on evaluating the end-to-end experience of exposing an existing AdventureWorks database through Data API Builder and consuming it from GitHub Copilot using SQL MCP Server. 

https://learn.microsoft.com/en-us/azure/data-api-builder/mcp/quickstart-visual-studio-code?tabs=stdio#step-2-configure-sql-mcp-server

For reference, I have also attached the configuration files generated during the setup, which can be used as a starting point for similar implementations.

Below is a sample of a query executed. During testing, GitHub Copilot was able to:

- Discover exposed entities automatically
- Understand table relationships
- Retrieve data from AdventureWorks database
- Generate contextual responses based on live database content

No custom prompts, embeddings, or API development were required.


https://github.com/user-attachments/assets/3b427b35-1841-4704-b1f2-f1bdd8eb4f62


## Why SQL MCP Server?
Traditional AI implementations against databases often fall into one of two approaches:
### Option 1: Vector Search    
Vector search enables AI to retrieve information using embeddings stored in a vector index. It is well suited for unstructured content such as documentation, knowledge bases, product descriptions, and semantic search scenarios.    
While effective for knowledge retrieval, it requires additional components such as embedding generation, vector storage, synchronization pipelines, and periodic re-indexing.    
### Option 2: Direct SQL Generation (NL2SQL)    
In this approach, an LLM generates SQL statements dynamically and executes them against the database. This provides flexibility for ad-hoc data exploration but introduces concerns around security, governance, query accuracy, resource consumption, and hallucinated SQL.    
### Option 3: SQL MCP Server
SQL MCP Server provides a governed middle ground for AI access to relational databases. Instead of generating arbitrary SQL or maintaining vector indexes, AI agents interact with approved database entities exposed through Data API Builder.  

Key benefits include:   
	- Real-time access to source data    
	- No embeddings or vector database required    
	- No synchronization or re-indexing overhead    
	- Built-in security and governance controls    
	- Consistent access through REST, GraphQL, and MCP   
  
This makes SQL MCP Server particularly well suited for operational and transactional data scenarios where accuracy, governance, and simplicity are critical.

## Real-World Use Cases

SQL MCP Server is particularly valuable in scenarios where AI agents need governed access to live operational data without exposing unrestricted SQL access.

Examples include:

- Customer support copilots retrieving customer orders and account information.
- Internal engineering assistants querying application inventory, deployment metadata, or operational dashboards.
- Business users interacting with sales, inventory, or financial data through natural language.
- AI agents performing database discovery and analysis tasks against approved datasets.
- Development teams using GitHub Copilot to explore database schemas and retrieve business data during application development.

In each of these scenarios, SQL MCP Server provides a controlled interface to enterprise data while preserving existing security and governance controls.

## Considerations

While SQL MCP Server simplifies AI-to-database integration, it is important to understand its intended scope.

- SQL MCP Server is designed for governed access to approved entities rather than unrestricted database administration.
- Complex analytical workloads may still require dedicated reporting or analytics platforms.
- Careful design of DAB entity exposure and permissions remains important to prevent overexposure of sensitive data.
- SQL MCP Server complements, rather than replaces, vector search solutions for unstructured content.

## Summary

SQL MCP Server provides a practical and governed approach for connecting AI agents to relational databases. By building on Data API Builder, it enables organizations to expose approved database entities as MCP tools while leveraging existing authentication, authorization, and governance controls.

In this walkthrough, I was able to expose an existing AdventureWorks database through REST, GraphQL, and MCP endpoints with minimal configuration and interact with the data directly from GitHub Copilot. The experience was straightforward, requiring significantly less effort than building custom APIs or implementing a vector search pipeline for structured data.

While vector search remains the preferred approach for unstructured content and knowledge retrieval, SQL MCP Server fills an important gap by providing secure, real-time access to operational and transactional data. As AI agents become increasingly integrated into development and business workflows, SQL MCP Server offers a compelling option for organizations looking to enable AI-driven data access without sacrificing governance, security, or control.

