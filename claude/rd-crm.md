# RD Station CRM - MCP Server

# RDQL Filtering Instructions for RD CRM
<rdql>
<context>
These instructions apply ONLY when using RD CRM MCP tools.

IMPORTANT: Use RDQL syntax ONLY when a tool has a filter parameter. Each tool's description specifies which fields are available for filtering.
</context>

## Basic Syntax
filter=field:value

## Operators
- Equals: status:won
- Not equals: -status:won
- Greater than: total_price:>100
- Less than: total_price:<100
- Greater or equal: total_price:>=100
- Less or equal: total_price:<=100
- IN (multiple values): status:(won,lost)
- NOT IN: -status:(won,lost)
- Pattern match (case-insensitive): name:~Test

## Data Types
- String: string or "string with spaces"
- Integer: 10
- Float: 10.5
- Date: 2023-01-01
- DateTime: "2023-01-01 12:00:00"
- Time: 12:00:00
- Array: (1, "2 b", 3c)

## Logical Operators
- AND (default): status:won total_price:>100
- OR: status:won or status:lost
- Grouping: (status:won or status:lost) and total_price:>100

## Custom Fields
Use @ prefix with field slug: @custom_field_slug:value

Examples:
- @department:technology
- -@active:true
- @priority:(high,medium)

## Examples
- Find won deals over R$1000: filter=status:won total_price:>1000
- Find contacts with name containing "John": filter=name:~John
- Multiple conditions: filter=(status:won or status:lost) and created_at:>=2023-01-01
</rdql>