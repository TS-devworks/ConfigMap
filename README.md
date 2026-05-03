# ConfigMap

A Zendesk admin tool to map, visualize, and analyze relationships across configuration objects. Understand dependencies, identify impact, and safely manage changes across your instance.

---

## Overview

ConfigMap provides a centralized interface to explore how Zendesk objects are connected. Search any object and instantly see where it is referenced, what it depends on, and how changes may affect other parts of your configuration.

Designed for impact analysis, debugging, and configuration auditing.

---

## Key Features

### Universal Search

* Search across all supported object types
* Query by name or ID
* Fast, debounced input for responsive results

---

### Relationship Mapping

* Bidirectional relationship visualization
* View both:

  * References (outgoing relationships)
  * Referenced By (incoming relationships)
* Set-based O(1) deduplication for performance

---

### Impact Analysis

* Summary cards showing dependency counts by type
* Quickly assess downstream effects before making changes

---

### Supported Object Types

* Triggers
* Automations
* Groups
* Macros
* Views
* SLA Policies
* Ticket Statuses
* Ticket Forms
* Ticket Fields
* Tags
* Brands

---

### Detailed Object View

* Type-specific metadata per object
* Conditions and actions (where applicable)
* SLA metrics table
* Admin Center deep links

---

### Filtering and Navigation

* Filter by object type
* Active / inactive toggle
* Click-through navigation between related objects

---

### Performance Optimizations

* In-flight request deduplication
* In-memory cache with 5-minute TTL
* requestIdleCallback for non-blocking relationship map generation
* Full pagination support across all API calls
* Console timing instrumentation for debugging

---

### Export

* Export full relationship map as JSON

---

## Architecture

Single-page Zendesk nav bar app with a two-panel layout:

* Left panel: searchable, filterable list of objects
* Right panel: selected object details and relationships

### Data Flow

1. Fetch Zendesk subdomain via ZAF
2. Execute all REST API calls in parallel
3. Cache results in memory (TTL-based)
4. Build relationship map during browser idle time

---

## Performance Details

* Cache key normalization ensures consistent cache hits
* In-flight promise deduplication prevents duplicate requests
* Set-based relationship linking replaces O(n) lookups
* Idle-time processing avoids UI blocking
* Debug logs prefixed for easy filtering in DevTools

