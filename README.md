# M365 Copilot Training — Debt Management Services, Consumer (Bajaj Finance Limited)

Training materials for a Microsoft 365 Copilot enablement session for the Bajaj Finance Limited (BFL) **Debt Management Services (DMS) — Consumer** team, delivered by Technizer India under the **GenAI for Enterprise Teams** program.

The session covers prompt engineering (meta-prompting and the RTCFT framework), Copilot in Excel (formulas and pivot tables), checking practice against a conduct standard in PDF, the end-to-end flow from a raw data file to a leadership-ready deck, and using Copilot Notebooks to work across more files than the chat attachment limit allows.

> All data in this repository is **synthetic** and safe to use in training. Customer names, account numbers and agency names are fictional. `DMS_Fair_Collection_Practices_Standard.pdf` is a **training sample**, not a BFL policy or a regulatory text.

## Contents

| File | Description |
|---|---|
| [`MetaPrompting_Guide_DMS.md`](MetaPrompting_Guide_DMS.md) | Introduces meta-prompting: asking Copilot to write your prompt for you. Includes six ready-to-use meta-prompts for DMS work. |
| [`BFL_DMS_MetaPrompts_Participant_Guide.md`](BFL_DMS_MetaPrompts_Participant_Guide.md) | Main hands-on guide. Six stages, each following the Meta Prompt → Generated Prompt → Live Apply rhythm: call documentation, account prioritisation, DMS performance reporting, roll-forward and recovery strategy, agency and conduct review, and a broken-PTP email in Outlook. Each stage lists what a good answer contains. |
| [`BFL_DMS_CopilotExcel_Participant_Guide.md`](BFL_DMS_CopilotExcel_Participant_Guide.md) | Copilot in Excel exercises: DPD bucket, risk score, days since PTP due and EMIs overdue formula columns, explaining a formula, and two pivot tables. |
| [`BFL_DMS_Alt_Copilot_Chat_Participant_Guide.md`](BFL_DMS_Alt_Copilot_Chat_Participant_Guide.md) | The same Excel exercises **without a Microsoft 365 Copilot licence**, for Copilot Chat users. You describe the sheet, Chat writes the formula, and you apply it. |
| [`Excel_To_PowerPoint.md`](Excel_To_PowerPoint.md) | "AI at Work" workbook describing a 9-step Copilot flow across three chats (Discovery, Execution, PowerPoint agent). Turns any file into an analysis, a Word document and a leadership deck, with a worked DMS example. |
| [`Copilot_Notebooks_Guide.md`](Copilot_Notebooks_Guide.md) | Using Copilot Notebooks as a persistent workspace. Add all files once as references, set standing instructions, and query across the call log, agency tracker, KPIs and the conduct standard without re-attaching. |
| [`copilot-pdf-playbook.md`](copilot-pdf-playbook.md) | Repeatable process for turning a large document into a formatted PDF using Copilot and Word, with a monthly agency review pack as the example. |
| [`DMS_Fair_Collection_Practices_Standard.pdf`](DMS_Fair_Collection_Practices_Standard.pdf) | Conduct standard (training sample) covering contact hours, agent conduct, agency governance, PTP handling, disputes, grievances and reporting. Used in Stage 5 and in the Notebooks exercises. |
| [`BFL_DMS_Copilot_Dataset.xlsx`](BFL_DMS_Copilot_Dataset.xlsx) | Practice dataset for the meta-prompt stages. Sheets: Call Interaction Log, Account Priority Matrix, DMS Performance, Bucket Trend Analysis, Recovery Strategy Tracker, Agency & Conduct Tracker. |
| [`BFL_DMS_Copilot_Demo.xlsx`](BFL_DMS_Copilot_Demo.xlsx) | Practice dataset for the Excel exercises: 25 accounts as of 30 Sep 2026, with columns N–Q left blank for Copilot-generated formulas. |
| [`PDFs/`](PDFs) | PDF versions of the seven guides, for printing or offline use. |
| [`Contact.md`](Contact.md) | Trainer contact details. |

## How to use this material

1. Start with `MetaPrompting_Guide_DMS.md` to learn the meta-prompt formula and RTCFT.
2. Work through `BFL_DMS_MetaPrompts_Participant_Guide.md` using `BFL_DMS_Copilot_Dataset.xlsx`.
3. Move to `BFL_DMS_CopilotExcel_Participant_Guide.md` for formula and pivot exercises on `BFL_DMS_Copilot_Demo.xlsx` (requires a Microsoft 365 Copilot licence).
   - **Copilot Chat only?** Use `BFL_DMS_Alt_Copilot_Chat_Participant_Guide.md` instead. The exercises are the same and no licence is required.
4. Practise the full 9-step flow in `Excel_To_PowerPoint.md`, from raw file to analysis, document and deck.
5. Use `Copilot_Notebooks_Guide.md` to bring everything into one Copilot Notebook, with no re-attaching and no 3-file limit.
6. Keep `copilot-pdf-playbook.md` for when a review pack needs to go out as a PDF.

## Requirements

- Microsoft 365 Copilot (Copilot Chat and Copilot in Excel and PowerPoint). Users with a basic licence can use Copilot Chat only, via `BFL_DMS_Alt_Copilot_Chat_Participant_Guide.md`.
- Access to Copilot Notebooks in the M365 Copilot app, for `Copilot_Notebooks_Guide.md`.
- The Excel files and the PDF uploaded to OneDrive, so they can be attached in Copilot Chat. BFL allows up to 3 attachments per prompt.

---

*Delivered by Technizer India | GenAI for Enterprise Teams*
