**Purpose**: Track implementation status and Bryan's questions for each feature.

**Status Legend**:

- ✅ **Implemented** - Fully functional (BE + FE)
- 🚧 **In Progress** - Partially built
- 📋 **Planned** - Designed, not started
- ❓ **Needs Clarification** - Questions for Bryan
- ❌ **Not Planned** - Not in scope

---
## Events Calendar

**Status**: ❓ Needs Clarification

**Figma Analyzed**:

- ✅ Events Calendar View - Monthly (August 2025)
- ✅ Events Calendar - List View (My Events - 436 total)

### UI Observations from Figma

**Calendar View (Monthly)**:

- Monthly calendar grid with event cards
- Event statuses: On Sale, Pre-Sale, Announced, Confirmed, Holds, Past, Canceled
- Example events: Billy Currington, William Clark Green, Ty Myers (all at Starlight Ranch)
- Filters: Search, Venue selector ("All Venue Selected"), Tags
- View toggles: List / Month
- "+ New Event" button

**List View**:

- Table columns: Event (photo + artist name + venue), Date, Time, Capacity, Ticket Price, Contacts, Venue
- "My Events" header with count: 436 total events
- Pagination: "Showing 09 / 436"
- All columns appear sortable (sort icons visible)
- Multiple contacts per event visible (Oliver.Jake, Thomas Joe shown)
- Pre-Sale status indicated by orange bar on left of row
- Artist photos displayed in Event column
- Same filtering available (Search, Filter By Venue, Filter By Tags)

### General Event System Questions

**Event Definition**:

- [ ] An "event" is a show/concert with an artist performing at a venue on a specific date?
- [ ] Is this tenant-specific or shared across tenants (central DB)?
- [ ] How does this relate to the existing `ViberateEvent` model (external API data)?
- [ ] Should Viberate events be importable into this calendar?

**Event Statuses** (from Figma legend):

- [ ] What's the difference between "On Sale" vs "Pre-Sale"?
- [ ] Who can change event status? (Only owner? Anyone with access?)
- [ ] What triggers status changes? (Manual only or automated?)
- [ ] "Holds" status - what does this mean? (Tentative date held for artist?)
- [ ] Can an event move backwards in status? (e.g., Confirmed → Pre-Sale)
- [ ] When does an event automatically become "Past"? (After event date?)

**Event Relationships**:

- [ ] Is an event REQUIRED to have an artist + venue? Or can it be just venue (open date)?
  > ⚠️ **Observation**: All events in Figma show artist + venue. Appears required.
- [x] ~~Can one event have multiple artists? (Multi-artist shows)~~
  > ✅ **ANSWERED**: YES! Lineup tab shows 5 artists on single event with defined roles
- [ ] Can one event span multiple venues? (Tour event vs single show)
- [ ] Can events have accommodations assigned?
- [x] ~~Link events to offers/contracts?~~
  > ✅ **ANSWERED**: YES! Offers tab exists on event detail page with 7 offers shown

### Add Event

**Status**: ❌ Not Implemented

**Required Fields** (updated from List View):

- [x] ~~Event date/time - single date or date range?~~
  > ✅ **Answered by List View**: Single date + single time (separate Date and Time columns: 22/09/2024, 10:00 PM EDT)
- [x] ~~Capacity/expected attendance?~~
  > ✅ **Answered**: Capacity is a dedicated column (shows values: 200, 400, 800, 340, 600)
- [x] ~~Ticket pricing information?~~
  > ✅ **Answered**: Ticket Price column exists (shows $ 200 for all visible events)
- [x] ~~Artist - required? Single or multiple?~~
  > ✅ **ANSWERED by Lineup Tab**: Events can have multiple artists with different roles
  > ✅ **Roles**: Headliner, Main Support Act, Special Guest, Opening Act, Emerging Artist
  > Example event shows 5 artists in lineup
- [ ] Venue - required?
  > ✅ **Partial Answer**: Venue shown in 2 places: under artist in Event column + dedicated Venue column
  > ✅ **Appears required** based on UI prominence
  > ❓ **Still Need**: Can one event span multiple venues?
- [ ] Event name/title - auto-generated from artist name or custom?
  > ❓ **New Question**: List shows "Charley Crockett" as event name - is this always the artist name or can events have custom titles (e.g. "Summer Music Festival")?
- [ ] Event status - default status on creation?
  > ⚠️ **Observation**: All visible events show "Pre-Sale" status - is this the default for new events?

**Contact Assignment** (NEW from List View):

- [x] ~~Event contacts - can events have multiple contacts?~~
  > ✅ **Answered**: Contacts column shows multiple names (Oliver.Jake, Thomas Joe on each event)
- [x] ~~What types of contacts?~~
  > ✅ **ANSWERED by Financial Tab**: Persons with Company affiliations shown
  > ✅ Two tabs visible: "Contacts" and "Team Members" - suggests role differentiation
- [ ] Can contacts have specific roles per event? (Promoter, Stage Manager, Booking Agent, etc.)
  > ⚠️ **Observation**: Financial tab shows company names like "EVENTful Moments", "Iconic Event planners" - suggests roles
- [x] ~~Are these selectable from tenant's address book or event-specific entries?~~
  > ✅ **Likely Answer**: Selectable from Address Book (Person + Company models confirmed to exist)

**Optional Fields** (still need clarification):

- [x] ~~Event tags~~
  > ✅ **CONFIRMED**: "Filter By Tags" option visible in calendar filters
  > ❓ Still need to know: What kind of tags? (Genre, type, internal categories?)
- [ ] Event photo/poster - or does it automatically use artist photo?
  > ⚠️ **Observation**: List view shows artist photos - are these from Artist model or event-specific?
- [ ] Doors time vs show time?
  > ❓ **Question**: "Time" column shows 10:00 PM EDT - is this doors or show time? Need separate fields?
- [x] ~~Supporting acts/openers?~~
  > ✅ **ANSWERED**: YES! Lineup shows: Main Support Act, Special Guest, Opening Act, Emerging Artist roles
- [x] ~~Event description/notes?~~
  > ✅ **CONFIRMED**: "Notes" tab exists on event detail page

**Behavior**:

- [ ] Can users create events without confirmed artist/venue?
- [ ] Default status when creating new event?
- [ ] Duplicate event functionality needed?

### Event Templates

**Status**: ❌ Not Implemented

**Questions**:

- [ ] Are templates in the Figma or was this removed from the navigation?
- [ ] If kept: What makes an event template? (Venue + standard contract terms?)
- [ ] Example use case: "Standard Friday night show at Starlight Ranch"?
- [ ] Who creates templates? (Admin only or all users with permission?)

### Event Pipeline

**Status**: ❌ Not Implemented

**From Figma Status Legend**:
Visible statuses suggest pipeline: `On Sale → Pre-Sale → Announced → Confirmed → Holds → Past → Canceled`

**Questions**:

- [ ] Is the pipeline linear or can events jump stages?
- [ ] What's the correct order? (Pre-Sale → Announced → On Sale → Confirmed?)
- [ ] Is "Pipeline" a kanban view of these statuses?
- [ ] Or is it a separate section from the calendar?
- [ ] Can users drag events between stages?

**Status Workflow**:

- [ ] Who can mark event as "On Sale"? (Requires ticket link/integration?)
- [ ] Who can "Confirm" an event? (Only event owner?)
- [ ] Can "Canceled" events be restored?
- [ ] What happens to "Past" events? (Auto-archive or stay visible?)

### Archived Events

**Status**: ❌ Not Implemented

**Questions**:

- [ ] Do "Past" events auto-archive after X days/months?
- [ ] Or is archiving separate from "Past" status?
- [ ] Can archived events be restored to active calendar?
- [ ] Are archived events searchable?
- [ ] Purpose of archiving vs just filtering by date range?

### Incoming Events

**Status**: ❌ Not Implemented

**Questions**:

- [ ] Not visible in Figma calendar - what are these?
- [ ] Event requests from venues? (Venue wants to book an artist)
- [ ] Event proposals from promoters?
- [ ] Cross-tenant event invitations?
- [ ] Imported Viberate events pending review?
- [ ] Or is this feature removed from scope?

### Calendar Filtering & Search

**From Figma UI**:

**Venue Filter**:

- [x] ~~"All Venue Selected" dropdown - show events from all venues or filter to specific venues?~~
  > ✅ **CONFIRMED**: Dropdown exists labeled "All Venue Selected" and "Filter By Venue"
  > ❓ Still need to know: Filter to venues tenant has access to? Or venues where tenant has events?
- [ ] Does this filter to venues the tenant has access to?
- [ ] Or venues where tenant has events?

**Tag Filter**:

- [x] ~~What tags can be applied to events?~~
  > ✅ **CONFIRMED**: "Filter By Tags" option exists in calendar
  > ❓ Still need to know: Genre, event type, internal categories? Pre-defined or user-created?
- [ ] Who creates tags? (Pre-defined or user-created?)
- [ ] Multiple tags per event?
- [ ] Tag taxonomy/structure?

**Search**:

- [x] ~~Search by what fields?~~
  > ✅ **CONFIRMED**: Search box visible in calendar view
  > ❓ Still need to know: Which fields? (Event name, artist name, venue name? All fields?)

**View Modes**:

- [x] ~~"List" view - what columns/fields shown?~~
  > ✅ **Answered**: Columns are: Event (photo+artist+venue), Date, Time, Capacity, Ticket Price, Contacts, Venue
  > ✅ All columns have sort icons (sortable)
- [ ] Can users customize list view columns? (Show/hide, reorder?)
- [ ] Can users adjust column order via drag/drop?
- [ ] Export to CSV/Excel from list view?
- [ ] Print calendar functionality?

**Pagination** (NEW from List View):

- [x] ~~Is there pagination for large event lists?~~
  > ✅ **Answered**: Shows "Showing 09 / 436" at bottom
- [ ] How many events per page? (9 shown in screenshot - is this the default page size?)
- [ ] Pagination style: page numbers, infinite scroll, or load more button?
- [ ] Can users adjust items per page (e.g., 10, 25, 50, 100)?

**"My Events" Concept** (NEW observation):

- [ ] What makes an event "My Event"? (Events I created? Events with my artists? Events I'm assigned to as contact?)
- [ ] Is there an "All Events" view showing entire tenant's events?
- [ ] Can users filter between "My Events" and "All Events"?
- [ ] Does count (436) reflect all my events or just filtered results?

### Event Detail View

**Status**: ✅ Financial & Lineup Tabs Analyzed

**Figma Analyzed**:

- ✅ Single Event Page - Financial
- ✅ Single Event Page - Lineup
- ✅ Single Event Page - Offers

**Event Header** (from Figma):

- Artist name + Status badge ("Hold" shown in yellow)
- Venue name below artist
- Share button + Actions dropdown (top right)
- Back arrow navigation

**Tab Navigation** (confirmed):

- [x] ~~What tabs are on event detail page?~~
  > ✅ **Answered**: Lineup, Offers, Financial, Notes, Assets, Tasks, Chat

**Financial Tab Details**:

**Show Health Panel** (Left Side):

- **Tickets Sold**: Progress bar showing 60% (1200 sold / 2000 capacity)
- **Gross Income**: Progress bar showing 85% ($3500 Forecast / $20000 Actual)
  > ❓ **Question**: How is "Forecast" calculated vs "Actual"?
- **Contacts Section**: Shows contacts with tabs (Contacts, Team Members)
  - Displays contact initials, name, company affiliation
  - Example: "Oliver.Jake - EVENTful Moments", "Jack Connor - Iconic Event planners"
    > [x] ~~What types of contacts?~~
    > ✅ **Answered**: Contacts linked to companies (Person + Company relationship)

**Sales Breakdown Panel** (Right Side):

**Tixr Integration**:

- [x] ~~Ticketing platform integration?~~
  > ✅ **Answered**: Tixr integration shown with "Connected" status
- [ ] Can users connect/disconnect integrations from this page?
- [ ] Support for multiple ticketing platforms? (Eventbrite, TicketMaster, etc.)
- [ ] Real-time sync or manual refresh?

**Ticket Types & Pricing** (from breakdown table):

Columns: Type, Comps, Sellable, Sold, Ticket Price, Gross

Visible ticket types:

1. **GA - Presale**: 327 sold @ $35.00 = $11,445.00
2. **GA - Day of Sale**: 97 sold @ $40.00 = $3,880.00
3. **VIP - Presale**: 176 sold @ $65.00 = $11,440.00
4. **VIP - Day of Sale**: 10 sold @ $70.00 = $700.00
5. **Merch Life**: 02 sold @ $0.00 = $0.00
   - Special note: "Artist keeps 100% - $0 at settlement manual $75 addition per ticket"
6. **GA - 4 Pack Tickets**: 30 sold @ $120.00 = $3,600.00

**Totals**:

- Comps: 0
- Sellable: 0
- Sold: 642
- Gross: $31,065.00
- Ticket Sales Tax (8.25% Sales tax): -$2,367.54
- **Net Gross**: $28,697.46

**Questions about Financial Tracking**:

**Ticket Types**:

- [ ] Are ticket types pre-defined or custom per event?
- [ ] Who creates ticket types? (Event owner? Admin?)
- [ ] Can ticket types have early-bird pricing beyond Presale/Day of Sale?
- [ ] Maximum number of ticket types per event?
- [ ] Can ticket types be disabled/hidden after creation?

**Comps & Sellable**:

- [x] ~~What are "Comps"?~~
  > ✅ **FULLY ANSWERED by Single Offer Page**: Complimentary tickets! 30 comps shown in GA category
- [x] ~~What is "Sellable"?~~
  > ✅ **FULLY ANSWERED by Single Offer Page**: Sellable = Available - Comps - Kills
  > Example: 3500 available - 30 comps - 0 kills = 3470 sellable
- [ ] Why are both showing 0 in this example?
  > ⚠️ **Observation**: Event Financial shows 0, but Offer Financial shows actual numbers. Might be empty event?
- [x] ~~Is Sellable = Capacity - Sold - Comps?~~
  > ✅ **ANSWERED**: Sellable = Available - Comps - Kills (not minus Sold - that's remaining)

**Pricing Tiers**:

- [ ] "Presale" vs "Day of Sale" - automatic date-based switching or manual?
- [x] ~~Can one ticket type have multiple price points over time?~~
  > ✅ **CONFIRMED**: Yes! GA has both Presale ($35) and Day of Sale ($40), VIP has both ($65 and $70)
  > ❓ Still need to know: Automatic switching based on date or manual control?
- [x] ~~Multi-pack tickets shown?~~
  > ✅ **CONFIRMED**: "GA - 4 Pack Tickets" at $120.00 shown in breakdown
  > ❓ Still need to know: How are these configured?

**Special Ticket Types**:

- [x] ~~Can ticket types have $0 price?~~
  > ✅ **CONFIRMED**: "Merch Life" ticket type at $0.00 shown
  > ✅ Note says "Artist keeps 100% - $0 at settlement manual $75 addition per ticket"
  > ❓ Still need to know: How are these artist-specific revenue shares configured?
- [ ] "$75 addition per ticket" - is this a settlement adjustment or fee?
- [ ] Can other ticket types be $0? (Staff, Media passes, Comp tickets)

**Tax Calculation**:

- [x] ~~Tax rate shown?~~
  > ✅ **CONFIRMED**: 8.25% Sales tax shown in both Event Financial and Offer Financial
  > ❓ Still need to know: Configurable per event? Per venue? Auto based on location?
- [ ] Is this automatic based on venue location?
- [ ] Support for multiple tax jurisdictions? (City, State, Federal)
- [ ] Tax-exempt ticket types allowed?

**Financial Integration**:

- [x] ~~Can data be manually entered if no integration?~~
  > ✅ **CONFIRMED by Single Offer Page**: "+ New Income", "+ NewExpense", "+ Before Adjusted Deduction" buttons exist
  > ✅ This proves manual entry capability
- [ ] Is financial data pulled from Tixr API automatically?
  > ⚠️ **Observation**: Tixr shows "Connected" - suggests automatic pull
- [ ] Sync frequency? (Real-time, hourly, daily, manual)
- [ ] What happens if Tixr disconnects?
- [ ] Can manual and automated data coexist?

**Show Health Metrics**:

- [ ] "Forecast" - how is this set? (Manual entry? Historical data? Target?)
- [ ] Does forecast update automatically or manual only?
- [ ] Can users set custom health metrics/KPIs?
- [ ] Alerts/notifications when thresholds not met?

**Event Detail - General Questions**:

- [x] ~~Event timeline/activity feed?~~
  > ✅ **LIKELY**: "Chat" tab exists - probably activity feed/comments
  > ✅ **ALSO**: "Activity" tab exists on Single Offer Page - likely similar pattern
- [x] ~~File attachments?~~
  > ✅ **CONFIRMED**: "Assets" tab exists on event detail
  > ✅ **ALSO**: "Files" tab exists on Single Offer Page
- [x] ~~Notes tab?~~
  > ✅ **CONFIRMED**: "Notes" tab exists on both event and offer pages
- [x] ~~Tasks tab?~~
  > ✅ **CONFIRMED**: "Tasks" tab exists on event detail page
- [ ] Edit event inline or separate edit page?

---

### Lineup Tab

**Status**: ✅ Analyzed - **MAJOR DISCOVERY: Multi-Artist Events Confirmed!**

**Lineup Table Structure**:

Columns: Checkbox, Artist (photo + name), Type, Status, Guarantee

**Example Lineup** (5 artists on single event):

| Artist           | Type             | Status    | Guarantee |
| ---------------- | ---------------- | --------- | --------- |
| Charley Crockett | Headliner        | Confirmed | $10,000   |
| Mike Ryan        | Main Support Act | Confirmed | $10,000   |
| Wade Bowen       | Special Guest    | Confirmed | $10,000   |
| Kolby Cooper     | Opening Act      | Confirmed | $10,000   |
| Gavin DeGraw     | Emerging Artist  | Confirmed | $10,000   |

**Artist Type/Roles Identified**:

- Headliner
- Main Support Act
- Special Guest
- Opening Act
- Emerging Artist

**Lineup Management Questions**:

**Selection & Ordering**:

- [ ] What do the checkboxes enable? (Bulk status update? Bulk delete? Bulk payment tracking?)
- [ ] Can lineup order be changed via drag/drop?
- [ ] Is display order same as table order or configurable?
- [ ] Maximum number of artists per event?

**Artist Types/Roles**:

- [ ] Are these 5 roles the only options or can custom roles be created?
- [ ] Can one artist have multiple roles in same event?
- [ ] Do artist types affect anything? (Payment tier, billing order, marketing?)
- [ ] Can roles be changed after artist is added?

**Artist Status**:

- [ ] What are other possible statuses besides "Confirmed"? (Pending, Tentative, Declined, Cancelled?)
- [ ] Who can change artist status? (Only event creator? Anyone with manage permission?)
- [ ] Does individual artist status affect overall event status?
- [ ] Can confirmed artists be unconfirmed/removed?
- [ ] Notification when artist status changes?

**Guarantee (Artist Payment)**:

- [ ] All showing $10,000 - are these independently editable per artist?
- [ ] Currency support - USD only or multi-currency?
- [ ] Is guarantee amount linked to Offers tab?
- [ ] Can guarantee be percentage-based? (e.g., "50% of door sales", "$5k + 10% merch")
- [ ] Payment tracking: when is guarantee paid? (Deposit, day-of, post-event?)
- [ ] Does guarantee flow to invoicing system?

**Adding Artists to Lineup**:

- [ ] How are artists added? (Search from Artist Database? Manual entry? Invitation?)
- [ ] Can artists from different tenants be added? (Cross-tenant collaboration?)
- [ ] Can non-database artists be added? (One-off performers not in Artist model?)
- [ ] Artist availability checking? (Conflict detection with other events?)
- [ ] Bulk import of lineup? (CSV, copy from template?)

**Event Title with Multi-Artists**:

- [x] ~~How does event title work with multiple artists?~~
  > ⚠️ **Observation**: Event header shows "Charley Crockett" (the Headliner) despite 5 artists in lineup
  > ❓ **Question**: Is event title always the headliner's name, or can it be customized?
- [ ] If event title is custom, where does it show? (Only in lists/calendar?)
- [ ] Can events have zero headliners? (All opening acts for a venue event?)
- [ ] Can events have multiple headliners? (Co-headlining tour)

---

### Offers Tab

**Status**: ✅ Analyzed - **MAJOR DISCOVERY: Offers Pipeline & Artist Booking Workflow!**

**Offers Table Structure**:

Columns: Artist, Agency, Booking Agent, Venue, Guarantee, Offer Status

**Example Offers** (7 artists - MORE than the 5 in Lineup!):

| Artist           | Agency | Booking Agent  | Venue          | Guarantee | Offer Status     |
| ---------------- | ------ | -------------- | -------------- | --------- | ---------------- |
| Charley Crockett | UTA    | Joel Siviour   | Starlink Ranch | $10,000   | Offer Submitted  |
| Mike Ryan        | WME    | Steve Goodgold | Starlink Ranch | $12,000   | Agent Engaged    |
| Wade Bowen       | CAA    | Astralwerks    | Starlink Ranch | $11,000   | Ready To Confirm |
| Kolby Cooper     | WASS   | Steve Goodgold | Starlink Ranch | $8,500    | Offer Confirmed  |
| Gavin DeGraw     | WME    | Joel Siviour   | Starlink Ranch | $15,000   | Offer Lost       |
| Billy Currington | CAA    | Astralwerks    | Starlink Ranch | $10,000   | Agent Engaged    |
| Garry Allan      | UTA    | Steve Goodgold | Starlink Ranch | $10,500   | Offer Confirmed  |

**Pagination**: Shows "09 / 436" (same pattern as event list)

**Critical Discovery: Offers vs Lineup Relationship**

- [x] ~~How do offers relate to lineup?~~
  > ✅ **ANSWERED**: Offers are the booking pipeline BEFORE lineup confirmation!
  > **Key Insight**: 7 offers exist, but only 5 artists in confirmed lineup
  > Artists with "Offer Lost" or pending statuses not in lineup yet
- [x] ~~What is the offer workflow?~~
  > ✅ **ANSWERED**: Offer Status pipeline appears to be:
  >
  > 1. **Offer Submitted** (yellow) → 2. **Agent Engaged** (blue) → 3. **Ready To Confirm** (orange) → 4. **Offer Confirmed** (green)
  >    OR → **Offer Lost** (red) if unsuccessful

**Offer Status Types Identified**:

- **Offer Submitted** (yellow) - Initial offer sent to artist/agency
- **Agent Engaged** (blue) - Agent is reviewing/negotiating
- **Ready To Confirm** (orange) - Ready for final confirmation
- **Offer Confirmed** (green) - Offer accepted, becomes lineup
- **Offer Lost** (red) - Offer declined/withdrawn

**Agency & Agent Information**:

- [x] ~~What agencies are tracked?~~
  > ✅ **ANSWERED**: Artist booking agencies visible: UTA, WME, CAA, WASS
- [x] ~~Individual booking agents tracked?~~
  > ✅ **ANSWERED**: Yes - individual agents shown (Joel Siviour, Steve Goodgold, Astralwerks)

**Guarantee Amounts Vary**:

- [x] ~~Are guarantees different per offer?~~
  > ✅ **ANSWERED**: Yes! Range from $8,500 to $15,000
  > Different from Lineup tab where all showed $10,000
  > ❓ **Question**: Do guarantee amounts in Lineup reflect confirmed offer amounts?

**Questions About Offers System**:

**Offer Creation & Management**:

- [x] ~~How are offers created?~~
  > ✅ **ANSWERED by Offer Generator Page**: "+ New Offer" button on Offer Generator main page!
  > ✅ Offer Generator is standalone page in navigation
- [ ] Can one artist have multiple offers for same event? (Re-negotiation?)
- [ ] Who can create offers? (Event owner? Booking agents? Admin only?)
- [x] ~~Can offers be edited after submission?~~
  > ✅ **LIKELY**: Single Offer Page exists with full financial editing ("+ New Income", "+ NewExpense" buttons)
  > ⚠️ Still need to know: Can status/guarantee be changed after submission?
- [x] ~~Offer templates - pre-fill standard terms?~~
  > ⚠️ **Observation**: Database schema shows `offer_templates` table planned
  > ❓ Still need to know: Implemented in UI?

**Offer Status Workflow**:

- [ ] Is the status progression linear or can it skip stages?
  > ⚠️ **Observation**: Pipeline visualization shows linear flow, but "Offer Status" dropdown exists suggesting manual changes possible
- [x] ~~Who updates offer status?~~
  > ✅ **CONFIRMED**: "Offer Status" dropdown visible on Single Offer Page
  > ✅ Suggests manual control, at minimum
  > ❓ Still need to know: Can it be automated from agent responses too?
- [ ] Can "Offer Lost" be revived to a new offer?
- [ ] When does "Offer Confirmed" artist appear in Lineup tab?
  > ⚠️ **Observation**: 2 artists show "Offer Confirmed" but only 5 in lineup - sync unclear
- [ ] Can confirmed offers be unconfirmed?
- [ ] Notifications when offer status changes?

**Offer vs Lineup Sync**:

- [x] ~~Why 7 offers but only 5 in lineup?~~

  > ✅ **Partial Answer**: Only "Offer Confirmed" artists appear in lineup
  > Billy Currington & Garry Allan have "Offer Confirmed" but only Garry Allan in lineup screenshot
  > Gavin DeGraw has "Offer Lost" - makes sense not in lineup
  > ❓ **Question**: Is there a delay in sync or manual step to add confirmed offers to lineup?

- [ ] When offer is confirmed, does it auto-add to lineup?
- [ ] Can lineup artists exist without offers? (Direct booking?)
- [ ] If offer guarantee changes, does lineup update?

**Agency/Agent Data**:

- [ ] Is Agency pulled from Artist model or offer-specific?
- [ ] Is "Booking Agent" the agent's name or a contact Person?
- [ ] Can one offer have multiple agents? (Co-representing?)
- [ ] Agent contact information stored? (For communication?)

**Offer Details Not Shown**:

- [x] ~~What's in a full offer beyond guarantee?~~
  > ✅ **FULLY REVEALED by Single Offer Page**: Income breakdown, Expenses, Deductions, Breakeven calculations!
  > ✅ Priority field, Percentage field, Date Submitted, 2 Contacts
  > ✅ Tabs: Notes, Activity, Call, Email, Files, Financials
  > ❓ Still need to know: Contract terms, rider requirements, technical specs tracked separately?
- [x] ~~Offer expiration dates?~~
  > ✅ **CONFIRMED**: "Date Submitted" field exists (December 1, 2024 shown)
  > ❓ Still need to know: Expiration date separate from submission date?
- [ ] Counter-offer tracking?
- [x] ~~Offer history/version tracking?~~
  > ✅ **LIKELY**: "Activity" tab exists on Single Offer Page - probably tracks changes
- [x] ~~Attached contract documents?~~
  > ✅ **CONFIRMED**: "Files" tab exists on Single Offer Page

**Venue Column Observation**:

- [x] ~~All shows same venue - is this because offers are event-specific?~~
  > ✅ **ANSWERED**: Yes, offers are per-event (all Starlink Ranch for this Charley Crockett event)
  > Makes sense - offering artists to perform at specific venue/event

**Bulk Actions**:

- [x] ~~Bulk selection available?~~
  > ✅ **CONFIRMED**: Checkboxes visible on Offer Generator main list
  > ❓ Still need to know: What actions? (Status update? Delete? Email?)
- [ ] Can multiple offers be sent at once? (Bulk submit?)
- [ ] Bulk status updates?
- [ ] Export offers list?

**Integration with Other Systems**:

- [ ] Do offers link to Invoices (when confirmed)?
- [x] ~~Email integration - send offers via email?~~
  > ✅ **CONFIRMED**: Email CRM tool exists in Offer Generator sidebar
  > ✅ **CONFIRMED**: "Email" tab exists on Single Offer Page
- [ ] E-signature for offer acceptance?
- [ ] Calendar invites on confirmation?

---

### Multi-Tenant Event Access

**Questions**:

- [ ] Are events tenant-specific or can they be shared?
- [ ] If Artist A (shared by Tenant 1 & 2) has an event, who sees it?
- [ ] Can multiple tenants collaborate on one event?
- [ ] Event ownership model? (Venue owner? Artist's primary agent?)

**Missing Permissions**:

- `view_events` - View event calendar
- `manage_events` - Create/edit events
- `view_event_lineup` - View lineup tab
- `manage_event_lineup` - Add/remove artists, change order
- `manage_artist_guarantees` - Edit artist payment amounts
- `confirm_lineup_artists` - Change artist status
- `view_event_offers` - View offers tab ✅ NEW from offers
- `create_event_offers` - Create offers for artists ✅ NEW from offers
- `manage_event_offers` - Edit/delete offers ✅ NEW from offers
- `change_offer_status` - Update offer workflow status ✅ NEW from offers
- `view_agent_information` - See agency/agent details ✅ NEW from offers
- `view_event_financials` - View financial tab
- `manage_event_financials` - Edit ticket types, pricing
- `view_event_health` - View show health metrics
- `manage_event_contacts` - Assign/manage event contacts
- `manage_event_templates` - Create event templates (if kept)
- `archive_events` - Archive past events
- `change_event_status` - Update event status
- `manage_event_tags` - Create/manage tags
- `manage_ticketing_integrations` - Connect/disconnect platforms
- `view_event_assets` - View assets tab (pending)
- `manage_event_tasks` - Manage tasks tab (pending)

**Database Schema Needed**:

```
events table:
- id, uuid
- title (nullable - might auto-populate from artist name)
- event_date (date) ✅ confirmed
- event_time (time) ✅ confirmed
- doors_time (time, nullable) - separate from event_time?
- status (enum: on_sale, pre_sale, announced, confirmed, holds, past, canceled) ✅ confirmed
- description (text, nullable)
- capacity (integer) ✅ confirmed (2000 capacity shown)
- tickets_sold (integer) ✅ NEW from financial (1200 sold)
- gross_forecast (decimal, nullable) ✅ NEW ($3500 forecast)
- gross_actual (decimal, nullable) ✅ NEW ($20000 actual)
- tax_rate (decimal, nullable) ✅ NEW (8.25% shown)
- net_gross (decimal, nullable) ✅ CALCULATED ($28,697.46)
- ticket_integration_platform (string, nullable) ✅ NEW (Tixr)
- ticket_integration_connected (boolean) ✅ NEW
- created_by (user_id)
- tenant_id (which tenant owns this)

event_ticket_types: ✅ NEW from financial tab
- id, uuid
- event_id (foreign key)
- name (string) - e.g., "GA - Presale", "VIP - Day of Sale"
- price (decimal) - e.g., $35.00, $65.00
- comps (integer) - complimentary tickets
- sellable (integer) - available to sell
- sold (integer) - tickets sold
- gross (decimal) - calculated total
- special_notes (text, nullable) - e.g., "Artist keeps 100%..."
- sort_order (integer)

event_offers: ✅ NEW from offers tab - booking pipeline
- id, uuid
- event_id (foreign key)
- artist_id (foreign key)
- agency_name (string) ✅ NEW - UTA, WME, CAA, WASS
- booking_agent_name (string) ✅ NEW - or person_id if linked to contacts?
- venue_id (foreign key) - though always same as event venue?
- guarantee_amount (decimal) ✅ - varies: $8,500 to $15,000
- offer_status (enum) ✅ NEW - offer_submitted, agent_engaged, ready_to_confirm, offer_confirmed, offer_lost
- submitted_at (timestamp)
- confirmed_at (timestamp, nullable)
- lost_at (timestamp, nullable)
- notes (text, nullable)
- created_by (user_id)

event_artists (pivot): ✅ confirmed from lineup tab
- event_id
- artist_id
- offer_id (foreign key, nullable) ✅ NEW - links to confirmed offer
- artist_type (enum) ✅ - headliner, main_support_act, special_guest, opening_act, emerging_artist
- status (enum) ✅ - confirmed, pending, tentative, declined (confirmed status shown)
- guarantee_amount (decimal) ✅ - artist payment ($10,000 shown, might come from offer)
- display_order (integer) - lineup order
- notes (text, nullable) - special arrangements

event_venues (likely belongs-to-one):
- event_id → venue_id (foreign key)

event_contacts (pivot): ✅ confirmed from financial tab
- event_id
- person_id (foreign key to Person) ✅ confirmed - shows Person + Company
- role (string, nullable) - "EVENTful Moments", "Iconic Event planners"
- contact_type (enum: contact, team_member) ✅ tabs shown

event_tags (pivot):
- event_id
- tag_id

tags table:
- id, name, type (event_tag)
```

**Relationships to Existing Models**:

- Events → Artists (many-to-many) ✅ **CONFIRMED from Lineup tab** - events can have multiple artists with roles
- Events → Venues (belongs-to-one based on UI)
- Events → Persons (many-to-many via event_contacts) ✅ confirmed - shows Person + Company
- Events → TicketTypes (one-to-many) ✅ NEW from financial tab
- Events → Accommodations (optional) - TBD
- Events → Offers (one-to-many) ✅ **CONFIRMED from Offers tab** - offers are booking pipeline before lineup
- Events → Files (polymorphic via Assets tab) - TBD
- Events → Comments (via Chat tab?) - TBD
- Events → Tasks (one-to-many via Tasks tab) - TBD

**Integration Relationships**:

- Events → Tixr Platform ✅ NEW (ticketing integration)

---

### Summary: What We Learned from Figmas

**✅ Confirmed from UI (8 Figmas analyzed)**:

**From Calendar & List Views**:

1. Events have: Date, Time, Capacity fields
2. Multiple contacts can be assigned
3. Events display with artist photo + name
4. Venue is prominently shown (appears required)
5. Events have statuses with colored indicators
6. List view has sortable columns
7. Pagination exists (09/436 format)
8. "My Events" filter exists

**From Financial Tab (NEW)**:

9. Event tabs confirmed: Lineup, Offers, Financial, Notes, Assets, Tasks, Chat ✅
10. Multiple ticket types per event (GA, VIP, multi-packs) ✅
11. Ticket pricing tiers (Presale vs Day of Sale) ✅
12. Financial metrics tracked (Forecast vs Actual, Net Gross) ✅
13. Tax calculation per event (8.25% shown) ✅
14. Ticketing platform integration (Tixr with Connected status) ✅
15. Contacts have company affiliations (Person + Company) ✅
16. Contact types: Contacts vs Team Members (separate tabs) ✅
17. Show Health dashboard with progress bars ✅
18. "Comps" and "Sellable" columns in sales breakdown ✅
19. Special ticket types with custom notes (Merch, artist revenue share) ✅
20. Ticket sales totals: 642 sold, $31,065 gross, $28,697.46 net ✅

**❓ Critical Questions Still Needed**:

**Event Structure**:

1. [x] ~~Can events have multiple artists (co-headliners)?~~
   > ✅ **MAJOR ANSWER from Lineup Tab**: YES! Events support multiple artists with defined roles
   > Example shows 5 artists: 1 Headliner + 4 supporting acts
2. Can events span multiple venues?
3. Event title: auto from artist or custom field?
4. What defines "My Events" vs "All Events"?
5. Default status for new events?
6. Doors time separate from show time?
7. Event templates - in scope or removed?
8. Link to existing Viberate Event data?

**Financial System (NEW from Financial tab)**:

9. How is "Forecast" set/calculated? (Manual entry? AI prediction? Historical?)
10. [x] ~~What are "Comps" exactly?~~
    > ✅ **ANSWERED by Single Offer Page**: Complimentary tickets that reduce sellable inventory
11. [x] ~~What is "Sellable"?~~
    > ✅ **ANSWERED by Single Offer Page**: Sellable = Available - Comps - Kills
12. Presale→Day of Sale: automatic date-based switch or manual?
13. Multi-platform integrations or Tixr only? (Eventbrite, TicketMaster?)
14. Tax rate: auto-calculated from venue location or manual per event?
15. Artist revenue share handling - how is "Merch Life" example configured?
16. Settlement tracking - is "$75 addition per ticket" an adjustment or fee?
17. Can financial data be manually entered if no integration?
18. Real-time sync frequency from Tixr?

**❓ Questions from Lineup Tab**:

19. Artist lineup order - drag/drop or manual sorting?
20. What do lineup checkboxes enable? (Bulk operations?)
21. Artist status options beyond "Confirmed"?
22. Is "Guarantee" linked to offers/contracts or separate?
23. Can guarantees include percentages or only flat fees?
24. How are artists added to lineup? (Search, invite, create new?)
25. Event title always uses headliner name or can be customized?
26. Can cross-tenant artists be added to lineup?

**❓ Questions from Event Offers Tab**:

27. [x] ~~How are offers created?~~
    > ✅ **ANSWERED by Offer Generator**: "+ New Offer" button on Offer Generator main page!
28. Is offer status progression linear or can skip stages?
29. When "Offer Confirmed", does it auto-add to Lineup tab?
30. Why do Billy Currington & Garry Allan have "Offer Confirmed" but one not in Lineup?
31. Can "Offer Lost" offers be resubmitted/revived?
32. Who updates offer status - manual or automated from agent responses?
33. Is Agency pulled from Artist model or entered per offer?
34. Is "Booking Agent" a Person contact or just a text field?
35. What's in a full offer beyond guarantee? (Terms, riders, technical specs?)
36. Offer expiration dates tracked?
37. Counter-offer negotiation supported?
38. [x] ~~Email/contract integration for sending offers?~~
    > ✅ **ANSWERED**: Email CRM tool exists in Offer Generator sidebar!

**❓ NEW Questions from Offer Generator Main Page**:

39. What fields are in "+ New Offer" form?
40. Can offers be created without an event first?
41. How does Venues filter work? (Show offers for selected venues only?)
42. How does Agencies filter work? (Show offers to/from selected agencies?)
43. What does Email CRM tool do? (Send offers? Track responses? Templates?)
44. What does Deal Tracker show? (Kanban board? Pipeline analytics?)
45. What Reports are available? (Conversion rate? Revenue forecast? Agent performance?)
46. How does Schedule Follow Ups work? (Automated reminders? Task creation?)
47. Bulk actions - what can be done with selected offers?
48. "All Offers 436" = same as "My Events 436" - is there 1 offer per event?
49. Can users view "My Offers" vs "All Offers"?
50. Integration between Offer Generator tools and Event tabs?

**❓ NEW Questions from Deal Tracker (Kanban View)**:

51. Drag-and-drop to change offer status? (Standard kanban behavior)
52. Where is "Offer Lost" status? (Separate column? Hidden from pipeline? Filter?)
53. "Deal Pipeline" dropdown - what other views? (By agent? By venue? Custom pipelines?)
54. Click offer card - opens detail modal or navigates to event?
55. Total deal value calculation per column? (Sum of all guarantees?)
56. Win rate analytics visible? (Confirmed vs Lost percentage?)
57. Time-in-stage tracking? (How long offer has been in current status?)
58. Can filter/search kanban view? (By venue, agency, date range?)
59. Sort cards within columns? (By date, guarantee, artist name?)
60. Bulk select cards and move to different status?
61. Archive cards from kanban view?
62. Card visual indicators beyond column? (Overdue, high-value, urgent?)
63. Column limits? (Max offers per stage, alerts when too many in one stage?)

**❓ NEW Questions from Single Offer Page (MAJOR)**:

64. [x] ~~What are "Comps"?~~

    > ✅ **ANSWERED**: Complimentary tickets that reduce sellable inventory

65. [x] ~~What is "Sellable"?~~

    > ✅ **ANSWERED**: Sellable = Available - Comps - Kills

66. What are "Kills"? (Unsellable seats? Obstructed view? Production holds?)

67. What is the "50%" field in Deal Terms? (Commission? Deposit? Revenue share?)

68. What are Priority levels? (Low, Medium, High, Urgent/Priority?)

69. Who can set offer priority? (Creator only? Manager?)

70. How is "Potential Artist Earning" calculated? (Guarantee + percentage of backend?)

71. How is "Venue Net Potential" calculated? (Formula?)

72. How is "Tickets to Breakeven" calculated? (Exact formula?)

73. Does breakeven update in real-time as financials change?

74. What expense types exist beyond "Fixed"? (Variable? Percentage-based?)

75. How are expenses allocated? (Venue vs Artist responsibility?)

76. "to be advanced per Artist" - expense settlement tracking?

77. Can multiple ticket types be combined in one row? (VIP & VIP DOS together)

78. Can users add custom income items beyond ticket types?

79. "Before Adjusted Deductions" - what are "after adjusted deductions"?

80. Tax calculation - per ticket type or on gross total?

81. What tabs exist on Single Offer Page? (Notes, Activity, Call, Email, Files, Financials - others?)

82. "Call" and "Email" tabs - integrated communication tracking?

83. Can offers be edited after submission? (Change guarantee, update financials?)

84. Does status pipeline at top allow clicking to change status?

85. Share button - generate shareable link? PDF export? Email to agent?

86. How do offer financials sync with Event Financial tab (if offer confirmed)?

**📋 Figmas Analyzed - Complete Set**:

- ✅ ~~Events Calendar - Monthly View~~ (COMPLETED)
- ✅ ~~Events Calendar - List View~~ (COMPLETED)
- ✅ ~~Single Event Page - Financial~~ (COMPLETED)
- ✅ ~~Single Event Page - Lineup~~ (COMPLETED - multi-artist confirmed!)
- ✅ ~~Single Event Page - Offers~~ (COMPLETED - booking pipeline revealed!)
- ✅ ~~Offer Generator - Main Page~~ (COMPLETED - central hub for all offers!)
- ✅ ~~Offer Generator - Deal Tracker~~ (COMPLETED - kanban pipeline view!)
- ✅ ~~Single Offer Page~~ (COMPLETED - financial modeling revealed!)

**Remaining Unknowns** (not in Figmas):

- "+ New Offer" form details
- ✅ ~~Deal Tracker interface~~ → **REVEALED**: Kanban board with 4 status columns!
- ✅ ~~Single Offer Page~~ → **REVEALED**: Full financial modeling with income/expenses/breakeven!
- Email CRM interface
- Reports interface
- Schedule Follow Ups interface
- Other event tabs: Notes, Assets, Tasks, Chat

---

## Pipeline & Offers

**Status**: ✅ Fully Designed (Figma Complete)

**Figma Analyzed**: ✅ Offer Generator Main Page

### Browse Offers & Single Offer Detail

**Status**: ✅ Fully Analyzed (Browse + Detail Page)

---

#### Single Offer Page - FULL FINANCIAL MODELING ✅

**Artist Example**: "Thirty Seconds to Mars" (Jared Leto)

**Page Header**:

- Artist photo + name
- "Offer Status" dropdown (shows "Confirmed")
- "Share" button
- Back arrow navigation

**Status Pipeline Visualization** (top of page):
Shows all 5 statuses as connected progress bar:

1. Offer Submitted
2. Agent Engaged ← **CURRENT STATUS** (highlighted in purple)
3. Ready To Confirm
4. Offer Confirmed
5. Offer Lost

**Tab Navigation**: Notes | Activity | Call | Email | Files | **Financials** (active)

---

**LEFT PANEL - Deal Terms**:

**Amount**: $100,000 (large display)

**Contacts**: 2 Contacts (with avatars)

**Priority**: Red "Priority" badge ✅ **NEW FIELD!**

- [ ] Priority levels: Low, Medium, High, Priority (urgent)?
- [ ] Who sets priority?
- [ ] Does priority affect anything? (Notifications, sorting, SLA?)

**Percentage**: 50% ✅ **NEW FIELD!**

- [ ] What is this 50%?
  - Commission percentage?
  - Deposit percentage required?
  - Revenue share?
  - Artist earning split?

**Date Submitted**: December 1, 2024

**Financial Details Panel**:

- **Offer Value**: $100,000
- **Potential Artist Earning**: $108,779
- **Venue Net Potential**: $27,194

**Breakeven Widget** (purple box):
"Tickets to Breakeven: **1,206** as offered"

- [ ] How is breakeven calculated?
- [ ] Is this (Expenses + Artist Guarantee) / Average Ticket Price?
- [ ] Does it update in real-time as income/expenses change?

---

**RIGHT PANEL - Financials Tab**:

### **Income Section** ✅ **CRITICAL - Answers Multiple Questions!**

**"+ New Income" button** (top right)

**Table Columns**: Item | Available | Comps | Kills | Sellable | Sales price | Total Price

**Ticket Types**:

| Item          | Available | Comps  | Kills | Sellable | Sales price | Total Price   |
| ------------- | --------- | ------ | ----- | -------- | ----------- | ------------- |
| GA            | 3500      | 30     | 0     | 3470     | $ 40        | $ 138,800     |
| VIP & VIP DOS | 300       | 0      | 0     | 300      | $ 100       | $ 30,000      |
| GA DOS        | 0         | 0      | 0     | 0        | $ 45        | $ 0           |
| **Total**     | **3800**  | **30** | **0** | **3770** |             | **$ 168,800** |

**MAJOR DISCOVERIES**:

- [x] ~~What are "Comps"?~~
  > ✅ **FULLY ANSWERED**: Complimentary tickets! 30 comps in GA category
  > These reduce the sellable inventory: Sellable = Available - Comps - Kills
- [x] ~~What is "Sellable"?~~

  > ✅ **FULLY ANSWERED**: Sellable = Available - Comps - Kills
  > GA example: 3500 available - 30 comps - 0 kills = 3470 sellable

- [x] ~~What are "Kills"?~~
  > ✅ **NEW DISCOVERY**: "Kills" column exists!
  > ❓ **Question**: What are kills? (Unsellable seats? Obstructed view? Held for production?)

**Income Calculation**:

- Total Price = Sellable × Sales price
- GA: 3470 × $40 = $138,800 ✅ correct!

**Ticket Types Shown**:

- GA (General Admission)
- VIP & VIP DOS (VIP + VIP Day of Sale combined?)
- GA DOS (Day of Sale) - shows 0 available (not created yet or sold out?)

---

### **Before Adjusted Deductions** ✅ **NEW SECTION**

**"+ Before Adjusted Deduction" button** (top right)

**Table Columns**: Item | Type | Percent | Amount | Total Price

**Example Row**:

- **Ticket Sales tax**: % of Gross | 8.25% | $ 3500 | **$ 138,800**
  - [ ] Why does tax total = GA total? ($138,800) Coincidence?
  - [ ] Is tax calculated on gross or per ticket type?

**Total After Deductions**: **$ 13,926**

- [ ] Math doesn't add up? $168,800 income - $138,800 tax = $30,000, not $13,926?
- [ ] Is there missing data or calculation error in Figma?

---

### **Expenses** ✅ **CRITICAL DISCOVERY**

**"+ NewExpense" button** (top right)

**Table Columns**: Item | Type | Amount | Quantity | Total Price

**Expense Line Items**:

| Item                                              | Type  | Amount  | Quantity | Total Price  |
| ------------------------------------------------- | ----- | ------- | -------- | ------------ |
| Additional Support                                | Fixed | $ 3,500 | 1        | $ 3,500      |
| House Costs                                       | Fixed | $ 7,500 | 1        | $ 7,500      |
| AV Production Rentals (to be advanced per Artist) | Fixed | $ 4,500 | 1        | $ 4,500      |
| **Total**                                         |       |         |          | **$ 15,500** |

**Expense Types**: "Fixed" shown - what other types?

- [ ] Variable expenses? (Per ticket sold?)
- [ ] Percentage-based? (% of gross sales?)

**Special Note**: "to be advanced per Artist" - indicates artist pays for this upfront?

- [ ] Are some expenses artist-responsibility vs venue-responsibility?
- [ ] Expense allocation/settlement tracking?

---

### **Financial Calculations Summary**:

Based on visible data:

- **Gross Income**: $168,800 (total ticket sales)
- **Tax Deduction**: Appears to be $138,800 (❓ needs clarification)
- **Expenses**: $15,500
- **Artist Guarantee**: $100,000 (from Deal Terms)
- **Potential Artist Earning**: $108,779 (shown in Financial Details)
- **Venue Net Potential**: $27,194 (shown in Financial Details)

**Questions about calculations**:

- [ ] How is "Potential Artist Earning" calculated? ($100k guarantee + backend points?)
- [ ] How is "Venue Net Potential" calculated? (Gross - Tax - Expenses - Artist Guarantee?)
- [ ] Breakeven at 1,206 tickets - how does this math work?
  - Total sellable = 3770 tickets
  - Breakeven = 1,206 tickets
  - Avg ticket price ≈ $44.74 ($168,800 / 3770)
  - 1,206 × $44.74 = $53,956 ≈ Artist Guarantee + some portion of expenses?

---

#### Browse Offers (Main List)

**Status**: ✅ Analyzed - Fully Designed

**Figma Page**: "Offer Generator" - "Quickly Create Tailored Offers that Captivate and Convert"

**Page Structure**:

**Left Sidebar - Browse & Tools**:

- **Browse Offers** (currently selected) - Main offers list
- **Other Tools**:
  - Email CRM
  - Deal Tracker
  - Reports
  - Schedule Follow Ups

**Main Content**:

- **Header**: "All Offers 436"
- **Filters**: Venues dropdown, Agencies dropdown
- **"+ New Offer" button** ✅ - This is how offers are created!
- **Bulk selection checkboxes**
- **Same offer table** as Event Offers tab

**Table Columns**: Artist, Agency, Booking Agent, Venue, Guarantee, Offer Status, Date

**Critical Discovery - Offer Generator is Central Hub**:

- [x] ~~What is an "offer"?~~
  > ✅ **FULLY ANSWERED**: Offer = booking proposal to artist/agency for specific event
  > Includes: Artist, Venue, Date, Guarantee amount, Agency/Agent info
- [x] ~~Who creates offers?~~
  > ✅ **ANSWERED**: Users click "+ New Offer" button on Offer Generator page
  > Likely booking agents/event managers with `create_event_offers` permission
- [x] ~~Is this related to events?~~
  > ✅ **ANSWERED**: YES! Each offer is for a specific event (all show Starlink Ranch/same date)
  > Offer Generator shows ALL offers across ALL events (436 total)
  > Event Offers tab shows only offers for THAT event

**Offer Generator vs Event Offers Tab**:

| Feature    | Offer Generator (Main Page)                  | Event Offers Tab             |
| ---------- | -------------------------------------------- | ---------------------------- |
| Scope      | ALL offers (436 total)                       | Only that event's offers (7) |
| Navigation | Standalone page in nav                       | Tab within event detail      |
| Filters    | Venues, Agencies                             | None (event-specific)        |
| Tools      | Email CRM, Deal Tracker, Reports, Follow Ups | Just offer list              |
| Create     | "+ New Offer" button                         | Likely links to main page    |

**Questions About Offer Generator**:

**Offer Creation**:

- [x] ~~How are offers created?~~
  > ✅ **ANSWERED**: "+ New Offer" button on Offer Generator page
- [ ] What does "+ New Offer" form look like? (Fields required?)
- [ ] Can offers be duplicated/templated?
- [ ] Bulk offer creation? (Send same offer to multiple artists?)

**Filtering & Search**:

- [ ] "Venues" filter - filter by which venue the offer is for?
- [ ] "Agencies" filter - filter by artist's agency?
- [ ] Search box functionality - search by artist, agent, status?
- [ ] Date range filtering?
- [ ] Status filtering (show only "Agent Engaged", etc.)?

**"Other Tools" - What are these?**:

**Email CRM**:

- [ ] What is Email CRM in context of offers? (Send offers via email? Track responses?)
- [ ] Integration with email providers?
- [ ] Email templates for offers?
- [ ] Track open/click rates?

**Deal Tracker**: ✅ **FULLY REVEALED IN FIGMA**

- [x] ~~What deals are being tracked?~~
  > ✅ **ANSWERED**: Offers across all pipeline stages!
- [x] ~~Kanban board of offer pipeline?~~
  > ✅ **CONFIRMED**: Classic kanban board with 4 columns matching offer statuses!

**Kanban Board Structure**:

Columns (left to right):

1. **Offer Submitted** (yellow/beige) - Badge count: 5
2. **Agent Engaged** (blue) - Badge count: 4
3. **Ready To Confirm** (orange) - Badge count: 3
4. **Offer Confirmed** (green) - Badge count: 4

**Offer Cards Display**:

- Artist photo
- Artist name
- Venue name
- Guarantee amount
- Date

**View Selector**: "Deal Pipeline" dropdown (suggests multiple pipeline views available)

**NEW Questions from Deal Tracker**:

- [ ] Drag-and-drop to change status? (Standard kanban UX)
- [ ] What other pipeline views exist in dropdown? (Custom pipelines? Agent-specific?)
- [ ] Column sorting - by date, guarantee amount, artist name?
- [ ] Card click - opens offer detail page or inline edit?
- [ ] Filter by venue/agency on kanban view?
- [ ] "Offer Lost" status - where does it show? (Separate column? Hidden?)
- [ ] Total deal value shown per column?
- [ ] Win rate analytics? (Confirmed vs Lost ratio)
- [ ] Time-in-stage tracking? (How long in "Agent Engaged"?)
- [ ] Card colors - any additional visual indicators beyond column?
- [ ] Bulk actions on kanban cards? (Select multiple, move together?)
- [ ] Can cards be archived from kanban view?

**Reports**:

- [ ] What reports are available? (Offer conversion rate? Artist response times?)
- [ ] Revenue projections from offers?
- [ ] Agent performance reports?
- [ ] Export capabilities?

**Schedule Follow Ups**:

- [ ] Automated reminders for pending offers?
- [ ] Follow-up task management?
- [ ] Integration with Tasks feature?
- [ ] Email scheduling?

**All Offers 436**:

- [x] ~~What does "436" represent?~~
  > ✅ **ANSWERED**: Total number of offers across all events
  > ⚠️ **Interesting**: Same number as "My Events" (436) - coincidence or offers = events?
- [ ] Are all 436 offers active or does this include archived/lost offers?
- [ ] Can users view "My Offers" vs "All Offers" (team-wide)?

**Bulk Actions**:

- [ ] What do checkboxes enable? (Bulk status update? Bulk delete? Bulk email?)
- [ ] Can select all filtered offers?
- [ ] Bulk export?

### Offer Generator - Create New Offer

**Status**: 📋 Designed (button exists, form not shown in Figmas)

- [x] ~~What does the generator do?~~
  > ✅ **ANSWERED**: "+ New Offer" button creates new offers
  > Likely a form to enter: Artist, Event/Venue, Date, Guarantee, Agency/Agent details

**Questions About Offer Creation Form**:

- [ ] What fields are required? (Artist, Event, Venue, Date, Guarantee mandatory?)
- [ ] How is Artist selected? (Dropdown from Artist Database? Search? Can create new?)
- [ ] How is Event selected? (Dropdown of events? Or create offer without event first?)
- [ ] Agency/Agent auto-populated from Artist data or manual entry?
- [ ] Guarantee amount - free entry or suggested based on artist tier?
- [ ] Offer templates - select from pre-built templates?
- [ ] AI-assisted - suggest guarantee based on historical data?
- [ ] Attach contract documents to offer?
- [ ] Set offer expiration date?
- [ ] Add custom terms/notes?
- [ ] Preview offer before submitting?
- [ ] Send offer immediately or save as draft?

### Offer Pipeline

**Status**: ✅ Fully Defined (from Event Offers Tab + Offer Generator)

- [x] ~~Pipeline stages?~~
  > ✅ **FULLY ANSWERED**:
  >
  > 1. **Offer Submitted** (yellow)
  > 2. **Agent Engaged** (blue)
  > 3. **Ready To Confirm** (orange)
  > 4. **Offer Confirmed** (green) → Becomes lineup
  > 5. **Offer Lost** (red) - Unsuccessful
- [x] ~~Kanban board view?~~
  > ✅ **FULLY CONFIRMED**: Deal Tracker provides kanban board with 4 status columns!
  > Columns: Offer Submitted (5) → Agent Engaged (4) → Ready To Confirm (3) → Offer Confirmed (4)
  > Cards show: Artist photo, name, venue, guarantee, date

**Questions**:

- [x] ~~Is "Deal Tracker" the kanban/pipeline view?~~
  > ✅ **CONFIRMED**: Yes! Classic kanban board with status columns
- [ ] Can users drag offers between status columns? (Likely yes - standard kanban UX)
- [ ] Status change triggers (manual drag, automated, email response)?
- [ ] SLA tracking (time in each stage)?
- [ ] Where does "Offer Lost" status show? (5th column? Separate view?)
- [ ] "Deal Pipeline" dropdown - what other views available?

### Archived Offers

**Status**: ❓ Not shown in Figmas

**Questions**:

- [ ] Does "All Offers" include archived offers or only active?
- [ ] Separate "Archived Offers" view or filter?
- [ ] What triggers archiving? (Offer Lost? Old Offer Confirmed? Time-based?)
- [ ] Can archived offers be restored?
- [ ] Archive navigation item exists in Bryan's list - where is it in UI?

**Missing Permissions** (updated with Offer Generator discoveries):

- `view_offers` - View offer generator page ✅ confirmed from figma
- `create_offers` - Click "+ New Offer" button ✅ confirmed
- `manage_offers` - Edit/delete offers ✅ confirmed
- `view_offer_pipeline` - View pipeline/deal tracker ✅ likely "Deal Tracker" tool
- `change_offer_status` - Update status workflow ✅ confirmed (overlaps with event permission)
- `bulk_manage_offers` - Use checkboxes for bulk actions ✅ confirmed
- `archive_offers` - Archive old offers (pending clarification)
- `access_email_crm` - Use Email CRM tool ✅ NEW from figma
- `access_deal_tracker` - Use Deal Tracker tool ✅ NEW from figma
- `view_offer_reports` - View Reports tool ✅ NEW from figma
- `schedule_followups` - Use Schedule Follow Ups tool ✅ NEW from figma
- `send_offers_via_email` - Email integration
- `filter_offers` - Use Venues/Agencies filters ✅ confirmed
- `view_offer_financials` - View Financials tab on Single Offer ✅ NEW from single offer
- `manage_offer_financials` - Edit income/expenses/deductions ✅ NEW
- `view_offer_breakeven` - See breakeven calculations ✅ NEW
- `set_offer_priority` - Change priority level ✅ NEW
- `track_offer_communications` - Use Call/Email tabs ✅ NEW
- `share_offers` - Use Share button ✅ NEW

**Database Schema Needed**:

Already defined in Events section as `event_offers` table ✅

Additional tables for Offer Generator tools:

```
email_crm_messages:
- id, offer_id
- subject, body
- sent_at, opened_at, clicked_at
- recipient_email

deal_tracker_stages: (if different from offer_status)
- Custom pipeline stages per tenant?
- ⚠️ May not be needed - "Deal Pipeline" dropdown might just be views of same offer_status data

deal_pipeline_views:
- id, name, tenant_id
- filter_config (JSON - venue, agency, date range filters)
- column_order
- created_by

offer_followups:
- id, offer_id
- scheduled_at, completed_at
- followup_type (email, call, etc.)
- assigned_to_user_id

offer_templates:
- id, name
- template_fields (JSON?)
- created_by

offer_income_items: ✅ **NEW from Single Offer Page**
- id, offer_id
- item_name (string) - "GA", "VIP & VIP DOS", "GA DOS"
- available (integer) - total tickets available
- comps (integer) ✅ CONFIRMED - complimentary tickets
- kills (integer) ✅ NEW FIELD - unsellable tickets
- sellable (integer) ✅ CALCULATED - available - comps - kills
- sales_price (decimal) - ticket price
- total_price (decimal) ✅ CALCULATED - sellable × sales_price
- sort_order (integer)

offer_deductions: ✅ **NEW from Single Offer Page**
- id, offer_id
- item_name (string) - "Ticket Sales tax"
- deduction_type (enum: percentage_of_gross, fixed) - "% of Gross"
- percent (decimal, nullable) - 8.25
- amount (decimal, nullable)
- total_price (decimal) - calculated deduction amount
- sort_order (integer)

offer_expenses: ✅ **NEW from Single Offer Page**
- id, offer_id
- item_name (string) - "Additional Support", "House Costs", etc.
- expense_type (enum: fixed, variable, percentage) - "Fixed" shown
- amount (decimal)
- quantity (integer) - for fixed expenses
- total_price (decimal) ✅ CALCULATED - amount × quantity
- notes (text, nullable) - "to be advanced per Artist"
- responsible_party (enum: venue, artist, split, nullable) - settlement tracking
- sort_order (integer)
```

**Updates needed to event_offers table** (from Single Offer Page):

```
Additional fields discovered:
- offer_value (decimal) ✅ - $100,000 (replaces guarantee_amount)
- potential_artist_earning (decimal) ✅ - $108,779 calculated
- venue_net_potential (decimal) ✅ - $27,194 calculated
- breakeven_tickets (integer, nullable) ✅ - 1,206 shown
- priority (enum: low, medium, high, urgent, nullable) ✅ - "Priority" badge
- percentage (decimal, nullable) ✅ - 50% (purpose unclear)
- date_submitted (date) ✅ - December 1, 2024
```

Relationships already confirmed:

- Offers → Events (many-to-one) ✅
- Offers → Artists (many-to-one) ✅
- Offers → Venues (many-to-one) ✅
- Offers → Income Items (one-to-many) ✅ NEW
- Offers → Deductions (one-to-many) ✅ NEW
- Offers → Expenses (one-to-many) ✅ NEW

**Dependencies**:

- Likely requires Events system first
- May require Contacts system enhancement
- Email notification system integration

---

## Summary: Key Discoveries & Questions for Bryan

### What We've Confirmed from Figma Analysis (8 screens)

**Events System**:

- ✅ Events have multiple artists with defined roles (Headliner, Main Support, Opening Act, etc.)
- ✅ Event statuses: On Sale, Pre-Sale, Announced, Confirmed, Holds, Past, Canceled
- ✅ Event tabs: Lineup, Offers, Financial, Notes, Assets, Tasks, Chat
- ✅ Financial tracking with ticketing integration (Tixr)
- ✅ Complex ticket types with Presale/Day of Sale pricing
- ✅ Comps and Kills inventory management
- ✅ Tax calculations and show health metrics

**Offers System** (**MAJOR DISCOVERY**):

- ✅ Offers are booking proposals to artists/agencies BEFORE confirming lineup
- ✅ Offer pipeline: Submitted → Agent Engaged → Ready To Confirm → Confirmed → Lost
- ✅ Full financial modeling PER OFFER (income projections, expenses, breakeven analysis)
- ✅ Offer Generator is central hub for all offers across all events
- ✅ Deal Tracker provides kanban pipeline view
- ✅ Individual offers track agency, booking agent, guarantee, priority
- ✅ Income breakdown: Available, Comps, Kills, Sellable, Price, Total
- ✅ Expense tracking with responsible party allocation
- ✅ Breakeven calculations ("1,206 tickets as offered")
- ✅ Communication tracking (Call/Email tabs on offer detail)

### Critical Questions for Bryan

**Events System**:

1. Can events span multiple venues? (Tour events)
2. Event title: auto-populated from headliner or custom field?
   > ⚠️ **Partial observation**: Event header shows "Charley Crockett" (headliner) despite 5 artists in lineup
3. What defines "My Events" vs "All Events"? (Created by user? Assigned to user?)
   > ⚠️ **Observed**: "My Events" header shows 436 total - but unclear what defines "mine"
4. Event templates - in scope or removed from navigation?
   > ⚠️ **Observation**: Listed in Bryan's navigation but not visible in any Figmas
5. How is "Forecast" calculated? (Manual entry? AI? Historical data?)
6. Presale→Day of Sale: automatic date-based or manual transition?
7. Multi-platform ticketing integrations? (Beyond Tixr: Eventbrite, TicketMaster?)
8. [x] ~~Tax rate: auto-calculated from venue location or manual per event?~~
   > ✅ **Partially answered**: 8.25% tax rate shown in both Event Financial and Single Offer
   > ❓ Still need to know: Is this auto-calculated or manual?

**Lineup System**:

9. Lineup order: drag-and-drop or manual field?
10. [x] ~~Artist statuses beyond "Confirmed"?~~
    > ✅ **Partially answered**: All lineup artists shown with "Confirmed" status
    > ❓ Still need to know: What other statuses exist? (Pending, Tentative, Declined, Cancelled?)
11. Can guarantees be percentage-based? (e.g., "50% of door sales" vs flat fee)
    > ⚠️ **Observation**: All shown as flat dollar amounts ($10,000), but 50% field exists on offers
12. Cross-tenant artists in lineup? (Collaboration scenarios)

**Offers System - Workflow**:

13. What is the "50%" field on offers? (Commission? Deposit? Revenue share?)
    > ⚠️ **Observed**: "Percentage: 50%" shown on Single Offer Page but purpose unclear
14. [x] ~~What are "Kills"?~~
    > ✅ **Partially answered**: "Kills" column confirmed in income breakdown (shows 0 in examples)
    > ❓ Still need to know: Purpose? (Unsellable seats? Obstructed view? Production holds?)
15. [x] ~~Priority levels definition?~~
    > ✅ **Partially answered**: "Priority" badge shown (red) on Single Offer Page
    > ❓ Still need to know: Full list of levels? (Low, Medium, High, Urgent/Priority?)
16. [x] ~~Is offer status progression linear or can stages be skipped?~~
    > ✅ **Partially answered**: Pipeline shown as: Submitted → Agent Engaged → Ready To Confirm → Confirmed or Lost
    > ❓ Still need to know: Can stages be skipped in either direction?
17. [x] ~~When "Offer Confirmed", does it auto-add artist to Lineup tab?~~
    > ✅ **Observation**: 7 offers exist, 2 are "Offer Confirmed", but only 5 in lineup
    > ❓ **Question**: Why Billy Currington & Garry Allan both "Offer Confirmed" but only one in lineup?
18. Can "Offer Lost" offers be resubmitted/revived?
19. Who updates offer status? (Manual only or automated from agent responses?)
    > ⚠️ **Observation**: Status dropdown exists on Single Offer Page, suggests manual control possible

**Offers System - Financial Modeling**:

20. How is "Potential Artist Earning" calculated? ($108,779 shown - is this guarantee + backend?)
    > ⚠️ **Data**: Offer Value $100,000, Artist Earning $108,779 → $8,779 difference unexplained
21. How is "Venue Net Potential" calculated? ($27,194 shown)
    > ⚠️ **Data**: Gross $168,800 - Tax $138,800? - Expenses $15,500 - Guarantee $100,000 = ?
22. Breakeven formula? (Appears to be based on expenses + guarantee / avg ticket price?)
    > ⚠️ **Data**: 1,206 tickets to breakeven, 3,770 total sellable, Avg price ~$44.74
23. [x] ~~What expense types beyond "Fixed"?~~
    > ✅ **Partially answered**: "Fixed" expense type shown with Amount × Quantity calculation
    > ❓ Still need to know: Variable (per ticket)? Percentage-based?
24. [x] ~~"Before Adjusted Deductions" - what are "after adjusted deductions"?~~
    > ✅ **Confirmed**: "Before Adjusted Deductions" section exists with tax calculations
    > ❓ Still need to know: What comes "after"? Another deduction section?
25. [x] ~~Artist vs Venue expense responsibility - how is this tracked and settled?~~
    > ✅ **Partially answered**: Note shown "to be advanced per Artist" on AV Production expense
    > ❓ Still need to know: Is this tracked systematically or just notes?

**Offer Generator Tools**:

26. [x] ~~Email CRM tool - functionality?~~
    > ✅ **Confirmed**: Email CRM tool exists in sidebar
    > ✅ **Confirmed**: Email tab exists on Single Offer Page for communication tracking
    > ❓ Still need to know: Send offers? Track opens/clicks? Templates?
27. [x] ~~Deal Tracker - drag-and-drop to change status?~~
    > ✅ **Confirmed**: Kanban board with 4 status columns (Submitted, Engaged, Ready, Confirmed)
    > ❓ Still need to know: Drag-and-drop enabled? (Standard kanban UX suggests yes)
28. [x] ~~Where does "Offer Lost" status show in kanban?~~
    > ✅ **Confirmed**: Only 4 columns visible (Submitted, Agent Engaged, Ready To Confirm, Confirmed)
    > ❓ **Question**: 5th "Offer Lost" column off-screen? Or separate view/filter?
29. [x] ~~"Deal Pipeline" dropdown - what other views available?~~
    > ✅ **Confirmed**: "Deal Pipeline" dropdown selector visible
    > ❓ Still need to know: What views? (By agent? By venue? Custom pipelines?)
30. [x] ~~Reports tool - what metrics?~~
    > ✅ **Confirmed**: "Reports" tool exists in sidebar
    > ❓ Still need to know: What reports? (Conversion rate? Revenue forecast? Agent performance?)
31. [x] ~~Schedule Follow Ups - automated reminders? Task creation?~~
    > ✅ **Confirmed**: "Schedule Follow Ups" tool exists in sidebar
    > ❓ Still need to know: Automated? Manual task creation? Integration with Tasks tab?
32. [x] ~~Bulk actions on offers - what's possible?~~
    > ✅ **Confirmed**: Bulk selection checkboxes visible on offer list
    > ❓ Still need to know: What actions? (Status update? Email? Delete? Archive?)

**Multi-Tenant & Access**:

33. If Artist A is shared by Tenant 1 & 2, who sees their events?
34. Can multiple tenants collaborate on one event?
35. Event ownership model? (Venue owner? Artist's primary agent?)

**Data Sync & Integration**:

36. How do offer financials sync with Event Financial tab when confirmed?
    > ⚠️ **Observation**: Offers have full financial modeling, Events have Financial tab - sync mechanism unclear
37. [x] ~~Real-time ticketing sync frequency from Tixr?~~
    > ✅ **Confirmed**: Tixr integration exists with "Connected" status shown
    > ❓ Still need to know: Real-time? Hourly? Daily? Manual refresh?
38. [x] ~~Can financial data be manually entered if no integration exists?~~
    > ✅ **Observation**: "+ New Income", "+ NewExpense", "+ Before Adjusted Deduction" buttons exist
    > ✅ This suggests manual entry capability
    > ❓ Still need to know: Can it coexist with integration or only one or the other?
39. Does Viberate event data link to this calendar system?

### Next Steps

1. Bryan review of questions above (39 total: 13 partially answered from Figmas, 26 still need clarification)
2. Clarify workflow priorities (Events first? Offers first? Parallel development?)
3. Define calculation formulas for financial projections
4. Confirm multi-tenant collaboration scenarios
5. Approve database schema for events and offers systems
6. Provide answers to the 13 partially-answered questions where we see the UI but don't know the behavior
