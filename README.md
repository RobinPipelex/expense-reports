# Expense Reports

Extract data from receipt PDFs and compile a structured expense report.

## What it does

Given a batch of receipt documents (PDFs), this method:

1. **Extracts pages** from each PDF using document extraction
2. **Analyzes each receipt** with vision AI to extract vendor, date, amount, currency, category, and payment method
3. **Compiles everything** into a structured expense report with line items, category breakdowns, totals by currency, and flagged items

## Input

| Variable | Type | Description |
|----------|------|-------------|
| `receipts` | `Document[]` | List of receipt PDF files |

## Output

An `ExpenseReport` with:
- Report title and date
- Total expenses and receipt count
- Line items (one per receipt) with vendor, date, amount, currency, category
- Category breakdown with subtotals
- Notes flagging mixed currencies, large expenses, or anomalies

## Usage

```bash
# Install
mthds install github.com/RobinPipelex/expense-reports

# Prepare inputs
mthds inputs

# Run
mthds run pipe .
```

## Pipes

| Pipe | Type | Description |
|------|------|-------------|
| `build_expense_report` | PipeSequence | Main orchestrator |
| `process_receipt` | PipeSequence | Per-receipt: extract + analyze |
| `extract_pages` | PipeExtract | PDF to pages |
| `analyze_receipt` | PipeLLM | Pages to structured ReceiptData |
| `compile_report` | PipeLLM | All receipts to ExpenseReport |
