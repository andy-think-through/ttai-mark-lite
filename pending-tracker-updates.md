# Pending Tracker Updates
## Date: 2026-04-17
## Run: scheduled (first Routine run)

### Northants Tracker

#### Companies
| Row (Company Name) | Column | Old Value | New Value |
|---|---|---|---|
| Hewlett & Sons Groundworks Ltd | Last Email # Drafted | 3 | 4 |
| Hewlett & Sons Groundworks Ltd | Date Email 4 Drafted | | 17/04/2026 |
| MBH Construction Ltd | Last Email # Drafted | 3 | 4 |
| MBH Construction Ltd | Date Email 4 Drafted | | 17/04/2026 |
| N R Groundworks Ltd | Last Email # Drafted | 3 | 4 |
| N R Groundworks Ltd | Date Email 4 Drafted | | 17/04/2026 |
| Brennan Building & Civil Engineering Ltd | Last Email # Drafted | 3 | 4 |
| Brennan Building & Civil Engineering Ltd | Date Email 4 Drafted | | 17/04/2026 |

#### Opportunities
No changes this run. Lead allocation (Overstone Hall, Irthlingborough, Ecton Brook, Middleton Cheney, 21 Townhouses, Weston, Modular Housing, Havelock Street) should be marked Allocated -> Sent once Andy sends the Gmail drafts.

#### Outreach_Log (New Rows)
| Date Drafted | Company Name | Contact Name | Email Address | Email # | Subject Line Used | Projects Included | Status |
|---|---|---|---|---|---|---|---|
| 2026-04-17 | Hewlett & Sons Groundworks Ltd | John Hewlett | info@hewlettandsons.co.uk | 4 | Last one from me -- Overstone Hall, Northampton | Overstone Hall 74 Dwellings, Irthlingborough 54 Dwellings | Approved |
| 2026-04-17 | MBH Construction Ltd | Anthony Lally | enquiries@mbh-construction.com | 4 | Last one from me -- Ecton Brook, Northampton | Ecton Brook 18 Affordable Homes, Middleton Cheney 54 Dwellings | Approved |
| 2026-04-17 | N R Groundworks Ltd | Nigel Roberts | enquiries@nrgroundworks.co.uk | 4 | Last one from me -- 21 Townhouses, Northampton | 21 Townhouses Northampton, Weston 6 New Homes | Approved |
| 2026-04-17 | Brennan Building & Civil Engineering Ltd | Robert Brennan | enquiries@bbandce.co.uk | 4 | Last one from me -- Modular Housing, Northampton | Boost TA Modular Housing, Havelock Street 5 Flats | Approved |

#### LinkedIn_Tasks (New Rows)
No new tasks

#### Daily_Batches
No changes

### Warwickshire Tracker

#### Companies
| Row (Company Name) | Column | Old Value | New Value |
|---|---|---|---|
| Tippercrete Concrete Ltd | Email Status | In Sequence | Warm |
| J&M Groundworks Coventry LTD | Email Status | Replied | Warm |

#### Blank Row Deletion (per Andy's instruction 16/04/2026)
973 blank rows identified in Companies tab. All have no Company Name but contain template data (Email Status = "In Sequence", Last Email # = 2, Date Email 2 Drafted = 2026-02-25). Andy instructed "Please delete blank rows" at 19:29 on 16/04/2026. Cowork process should delete these rows.

#### Opportunities
No changes

#### Outreach_Log (New Rows)
No new rows

#### LinkedIn_Tasks (New Rows)
No new tasks

#### Daily_Batches
No changes

### Flagged for Andy (require human decision)
1. **SRK Groundworks and Civils** -- Email Status = "Replied" (not valid per schema). No notes explaining the reply. Should this be Warm, or something else?
2. **JDW Brickwork & Construction Ltd** -- Josh Warren replied warm 30/03, call was scheduled. Only Andy can set In Conversation or Client. What's the current status?
3. **"Replied" status normalisation** -- "Replied" and "Replied -- Warm" are not valid Email Status values per tracker-schema.md. Valid options: New / Contacted / In Sequence / Warm / In Conversation / Opted Out / Bounced / Parked / Client. Recommend normalising J&M -> Warm (done above), SRK -> awaiting Andy's input.
4. **Re-engagement template missing** -- Andy requested re-engagement emails for A Valley Plant, M Carty, Kimben. No re-engagement template exists in `templates/`. Cannot draft without template. Please add or confirm substitute.
