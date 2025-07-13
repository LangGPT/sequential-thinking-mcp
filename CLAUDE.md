# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a Model Context Protocol (MCP) server that provides a sequential thinking tool for dynamic and reflective problem-solving. It's a TypeScript/Node.js project that implements an MCP server exposing a single `sequentialthinking` tool.

## Development Commands

### Build and Development
- `npm run build` - Compile TypeScript to JavaScript in `dist/` directory and make executable
- `npm run prepare` - Same as build (runs automatically on install)
- `npm run watch` - Watch mode compilation with TypeScript

### Docker
- `docker build -t mcp/sequentialthinking -f Dockerfile .` - Build Docker image

No test scripts are configured in this project.

## Architecture

### Core Components

**SequentialThinkingServer Class** (`index.ts:25-138`)
- Main server implementation that handles sequential thinking operations
- Manages thought history, branching, and validation
- Supports thought revision and branching functionality
- Handles environment-based logging control via `DISABLE_THOUGHT_LOGGING`

**MCP Server Setup** (`index.ts:244-285`)
- Uses `@modelcontextprotocol/sdk` for MCP protocol implementation
- Single tool endpoint: `sequentialthinking`
- Runs on stdio transport for MCP communication

### Key Features
- Dynamic thought progression with adjustable totals
- Thought revision and branching capabilities
- Visual formatting with chalk for console output
- JSON-based tool responses with metadata
- Environment variable control for logging

### Tool Schema
The `sequentialthinking` tool accepts:
- `thought` (required): Current thinking step
- `nextThoughtNeeded` (required): Boolean for continuation
- `thoughtNumber` (required): Current step number
- `totalThoughts` (required): Estimated total steps
- Optional parameters: `isRevision`, `revisesThought`, `branchFromThought`, `branchId`, `needsMoreThoughts`

## Configuration

**Environment Variables:**
- `DISABLE_THOUGHT_LOGGING=true` - Disables console output of formatted thoughts

**Dependencies:**
- `@modelcontextprotocol/sdk` - Core MCP framework
- `chalk` - Terminal colors and formatting
- `yargs` - Command line argument parsing

**Project Structure:**
- Single-file implementation in `index.ts`
- ESM module type with Node.js executable output
- TypeScript configuration extends parent `tsconfig.json`