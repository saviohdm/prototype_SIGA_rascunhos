# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This repository contains HTML prototypes for SIGA (Sistema Integrado de Gestão Administrativa), a legal case management system for the Brazilian Public Prosecutor's Office (Ministério Público da Bahia - MPBA). The prototypes focus on the electronic process drafts ("rascunhos") functionality.

## Repository Structure

The repository contains two main HTML prototype files:

- **Rascunho.html**: Full AngularJS-based draft management interface extracted from the production SIGA system. Shows the complete application structure with navigation, modals, and workflow components.
- **caixa_de_entrada.html**: Standalone prototype for the inbox/received processes interface. Implements a modern, responsive design with CSS Grid and clean UI components.

Supporting files include screenshot references (PNG images) that document the UI design requirements.

## Architecture & Technology Stack

### Rascunho.html (Production Template)
- **Framework**: AngularJS 1.x (`ng-app="boipeba"`)
- **UI Library**: Bootstrap 3.x with custom navbar components
- **Rich Text**: CKEditor for document editing
- **Key Controllers**:
  - `boipebaController`: Main application controller
  - `recebidosCtrl`: Manages draft processes and inbox functionality
- **Bundled Scripts**: jQuery, jQuery Validation, Angular, Bootstrap, custom controllers

### caixa_de_entrada.html (Prototype)
- **Pure HTML/CSS**: No framework dependencies
- **Layout**: CSS Grid for responsive filter forms
- **Design System**: CSS custom properties for theming
- **Color Scheme**: Brand blue (#2f7fc2), light backgrounds, green row highlights

## Key Functional Areas

### Draft Process Management ("Meus Rascunhos")
The system allows users to:
- Create, edit, sign, and delete process movement drafts
- Assign drafts to other users (members/servers)
- Reorder drafts within a process (move up/down)
- Sign multiple drafts and route them with a single action
- Attach documents (including Word Online integration)

### Process Movements
- Movement types based on CNMP (National Council of the Public Prosecutor's Office) classifications
- Internal movements with glossary descriptions
- Document complements using rich text editor with model templates
- CID (International Classification of Diseases) support for health-related processes
- Attachment management with reordering capabilities

### Routing & Workflow
- Immediate forwarding after movement (`StEncaminhar` flag)
- Assignment to organizational units or individuals
- "Apto" (ready/express) processing flag
- Draft vs. final movement states

## Common Development Context

### Navigation Structure
The main menu hierarchy follows MPBA organizational structure:
- Carreira (Career management)
- Secretaria (Administrative office)
- Corregedoria (Internal affairs/oversight)
- Comunicação (Communications)
- Conselho Superior (Superior council)
- Ouvidoria (Ombudsman)
- Promotorias (Prosecutor offices)
- Gestão Estratégica (Strategic management)
- Tabelas Básicas (Master data tables)
- Consulta (Queries/searches)
- Relatórios (Reports)
- Processos (Electronic processes)
- Pagamento (Payments)

### Modal Patterns
The application uses Bootstrap modals extensively for:
- Draft assignment (`idAtribuirRascunhoProcessoMovimentoModal`)
- Process movement (`movimentarProcessoModal`)
- Destination selection (`idDestinoMovimentoRascunhoModal`)
- Digital signature (`assinarModal`)

### State Management
Process movements track several states:
- `StCheck`: Selection checkbox state
- `StEncaminhar`: Forward immediately flag
- `StExpresso`: Express/ready processing
- `StCID`: CID classification required
- `StDespacharLote`: Batch dispatch enabled
- `StCaraterRelevancia`: Importance/relevance flag

## Design Patterns

### Process Display
Processes are shown with accordion panels grouped by case, displaying:
- Process number and year format: `{Numero} / {Ano}`
- CNMP subject classification
- Involved parties concatenated
- Badge with draft count
- Link to open full process view

### Draft Items
Each draft row contains:
- Up/down reorder controls
- Selection checkbox
- Timestamp (formatted with `jsdatetimeutc` filter)
- Movement type from CNMP classification
- Author/creator name
- Edit action icon

### Filter/Search Components
The inbox prototype demonstrates standard search patterns:
- SIGA/SIMP process number search
- Involved party name search
- Sort order toggle (oldest first)
- Attached/appendix process toggle
- Results pagination with count badges
