# 1. Introduction

This document outlines the complete fullstack architecture for Facemake v3, including backend systems, frontend implementation, and their integration. It serves as the single source of truth for AI-driven development, ensuring consistency across the entire technology stack.

Following **Clean Architecture** principles from iOS best practices and **serverless patterns** from Vercel/Supabase integration, we achieve clear separation of concerns while maintaining the radical simplicity required by the PRD.

## Starter Template
N/A - Greenfield project. Building with:
- **iOS Frontend:** Native SwiftUI following Clean Architecture patterns
- **Backend:** Vercel Edge Functions + Supabase (Auth, Database)
- **AI Service:** Google Gemini 2.5 Flash (image generation preview)
