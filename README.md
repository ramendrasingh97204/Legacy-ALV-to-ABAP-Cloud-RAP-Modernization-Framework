# Legacy ALV to ABAP Cloud RAP Modernization Framework

This repository is a reference implementation for modernizing a legacy SAP ALV-based report into an ABAP Cloud RAP (RESTful ABAP Programming Model) architecture.

The sample is centered on a process-order detail scenario and demonstrates how classic report logic, selection-screen components, and database-driven data can be structured into CDS views, behavior definitions, service exposure, and supporting ABAP classes.

## Overview

The repository provides a practical migration pattern for:

- Legacy ALV report logic
- SAP table-based data extraction
- CDS-based read models and projections
- RAP business behavior definitions
- Service exposure for OData consumption
- Helper classes for process logic and text retrieval

## Why this project exists

Many SAP applications still rely on classical ALV reports built with selection screens and includes. This project shows a structured transition path to ABAP Cloud and RAP by separating concerns into:

- Data retrieval and presentation
- Behavior logic
- Business object modeling
- Service definition exposure

## Repository structure

```text
.
├── ALV programs/
│   ├── includes/
│   │   ├── zram_process_order_details_sel/
│   │   ├── zram_process_order_details_sub/
│   │   └── zram_process_order_details_top/
│   └── programs/
│       └── zram_process_order_details/
│           └── zram_process_order_details.asprog
├── Behaviour Defination/
│   ├── zi_ram_processorderdetail/
│   └── zc_ram_processorderdetail/
├── CDS View/
│   ├── za_ram_actual_cost_var/
│   ├── zi_ram_processorderdetail/
│   ├── zc_ram_processorderdetail/
│   ├── zr_ram_processorderdetail/
│   ├── zr_ram_processorderstatus_tf/
│   ├── zr_ram_reservation/
│   └── zr_ram_reservation_tf/
├── Classes/
│   ├── zbp_i_ram_processorderdetail/
│   ├── zcl_ram_process_order/
│   └── zcl_ram_read_text/
├── Metadata file/
│   └── zc_ram_processorderdetail.asddlxs
├── Service/
│   └── zui_ram_processorder.assrvds
├── RAP Naming Convention.pdf
├── New Microsoft Excel Worksheet.xlsx
└── README.md
```

## Key artifacts

### 1. ALV report
The sample report is implemented as a classical ALV program:

- `ALV programs/programs/zram_process_order_details/zram_process_order_details.asprog`

This program:

- initializes selection logic
- retrieves data
- invokes ALV generation

### 2. CDS views
The project includes several CDS views for different layers of the RAP model, including:

- `Zi_Ram_ProcessOrderDetail` — root entity / interface view
- `Zc_Ram_ProcessOrderDetail` — consumption/projection layer
- supporting views for reservations, process-order status, and actual cost variants

These views encapsulate the underlying business data and provide the modeling foundation for the RAP service.

### 3. Behavior definition
The behavior definition is defined for the interface view:

- `Behaviour Defination/zi_ram_processorderdetail/zi_ram_processorderdetail.asbdef`

It includes a custom action:

- `UpdateCostingVariant`

This demonstrates how business actions can be exposed through the RAP behavior layer.

### 4. Service definition
The service definition exposes the consumption entity:

- `Service/zui_ram_processorder.assrvds`

```abap
@EndUserText.label: 'Service defination Process Order'
define service ZUI_RAM_ProcessOrder {
  expose ZC_Ram_ProcessOrderDetail;
}
```

### 5. Supporting classes
The classes folder contains implementation support for:

- process-order logic
- text retrieval
- behavior class implementations

This is typical of a RAP application where business logic is split between CDS and ABAP classes.

## Sample data model focus

The objects are modeled around process-order details, including fields such as:

- process order number
- work center
- plant / supply area
- operation details
- reservation data
- product text
- process order status
- costing-related information

This makes the repository a useful template for transforming operational monitoring/reporting screens into RAP-based services.

## Typical modernization flow

1. Start with a legacy ALV report
2. Identify the data extraction and business logic
3. Move the domain model into CDS views
4. Create a RAP behavior definition
5. Expose the object through a service definition
6. Add ABAP classes for behavior and helper logic
7. Consume via Fiori/OData or SAP UI clients

## Suggested usage

This repository is best used as a reference or starter pattern for:

- SAP S/4HANA Cloud or ABAP Cloud RAP adoption
- ALV-to-RAP modernization initiatives
- internal business object modeling exercises
- process-order and manufacturing reporting scenarios

## Prerequisites

To use or extend this project in an SAP development environment, you should have:

- SAP S/4HANA or ABAP Cloud development system
- ABAP development tools (ADT)
- knowledge of CDS, RAP, and ALV programming
- access to process-order related business data in the target system

## Notes

This project is designed as a framework/template for modernization rather than a finished business application. It illustrates the key design shift from classic ALV reporting toward modern RAP services.

## Future extensions

Possible enhancements include:

- stricter authorization checks
- more comprehensive business validations
- OData UI annotations
- Fiori Elements adaptation
- additional entities and associations
- test classes and automation coverage

## License

No explicit license file is present in the repository at this time. If this project is intended for reuse, add a license file such as MIT or Apache 2.0 before public distribution.
