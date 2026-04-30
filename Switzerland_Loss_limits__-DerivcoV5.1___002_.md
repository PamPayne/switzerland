---
country: Switzerland
document_name: Switzerland Loss limits
source_file: Switzerland_Loss limits_ -DerivcoV5.1_ (002).pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# Switzerland Loss limits

Derivco - Internal

Author: Regulated markets

Release Date  
25 March 2020

Copyright © Derivco 2020 confidential  
© 2020 Derivco (Pty) Ltd All Rights Reserved  
This document is intended for the use of Derivco (Pty) Ltd only. It contains information that is privileged and that is the intellectual property of Derivco (Pty) Ltd. You may neither copy nor use it, nor disclose it to anyone else. If you have received this document in error, please notify us immediately.

## Revision History

Derivco - Internal

| Revision | Date | Changed By | Comments/Reasons |
|---|---|---|---|
| 1 | 2/3/2020 | Werner Erasmus | Created |
| 2 | 4/3/2020 | Marianne Ryder | Added legislation, glossary and test cases, DOS Business rules, Back Office, reporting |
| 3 | 17/3/2020 | Marianne Ryder | Updated with DOS feedback |
| 4 | 19/3/2020 | Marianne Ryder | Derivco Review |
| 5 | 23/03/2020 | Marianne Ryder | Derivco Review 2 |
| 6 | 24/03/2020 | Marianne Ryder | Restructured document to have each rule in the relevant section and specifying what will be done |
| 7 | 27/03/2020 | Marianne Ryder | Updated with DOS comment, added sign-off |

Copyright © Derivco 2020 confidential  
© 2020 Derivco (Pty) Ltd All Rights Reserved  
This document is intended for the use of Derivco (Pty) Ltd only. It contains information that is privileged and that is the intellectual property of Derivco (Pty) Ltd. You may neither copy nor use it, nor disclose it to anyone else. If you have received this document in error, please notify us immediately.

## Table of Contents

- REVISION HISTORY
- TABLE OF CONTENTS
- LIST OF FIGURES
- LIST OF TABLES
- INTRODUCTION
- GLOSSARY
- LEGISLATION
- SWITZERLAND LOSS LIMITS
- BUSINESS RULES
- CORE FUNCTIONALITY
  - Setting Loss limits
  - Tracked Value/Usage
  - Reset of loss limit.
  - Core Test Cases
- BONUS TO CASH – PLAYTHROUGH
  - Bonus Flush Test Cases
- WITHDRAWALS/CASHINS
  - CAWs/User Refund Tokens – To be confirmed by DOS
  - Mistakenly flushed
  - Withdrawals Test Cases
- GENERATED EVENTS
  - Event on limit set
  - Event on limit reached
- RESPONSIBLE GAMING
  - Player Message
  - Loss limit information
- BACK OFFICE
- APPENDIX A – TEST CASES
- APPENDIX B – DOS USE CASES

## List of Figures

- FIGURE 1 CORE FUNCTIONALITY REQUIREMENTS AND CURRENT FUNCTIONALITY
- FIGURE 2 SETTING LOSS LIMITS REQUIREMENTS AND CURRENT FUNCTIONALITY
- FIGURE 3 TRACKED VALUE REQUIREMENTS AND CURRENT FUNCTIONALITY
- FIGURE 4 RESET LOSS LIMIT REQUIREMENT AND CURRENT FUNCTIONALITY
- FIGURE 5 BONUS TO CASH REQUIREMENT AND CURRENT FUNCTIONALITY
- FIGURE 6 LOSS LIMIT RESET
- FIGURE 7 RESET LOSS LIMIT ON FLUSHED CASHIN
- FIGURE 8 EVENT INSIGHT REQUIREMENT AND FUNCTIONALITY
- FIGURE 9 PLAYER ALERT REQUIREMENT AND CURRENT FUNCTIONALITY
- FIGURE 10 BACKOFFICE REQUIREMENTS AND CURRENT FUNCTIONALITY

## List of Tables

- TABLE 1 GLOSSARY OF TERMS
- TABLE 2 DOS BUSINESS RULES
- TABLE 3 SETTING LOSS LIMITS EXAMPLE
- TABLE 5 TRACKED VALUE EXAMPLE
- TABLE 6 PLAYTHROUGH EXAMPLE
- TABLE 7 CASHIN PROCESS FLOW
- TABLE 8 EXAMPLE OF EVENT ON LIMIT REACHED
- TABLE 9 DERIVCO TEST CASES

## Introduction

This document is the result of workshops between DOS and Derivco in the week 24 February – 28 February 2020 to define the delivery of the loss limit functionality. The scope needs to be agreed with DOS and Derivco before development can commence.

## Glossary

As per DOS document. Some changes made.

### TABLE 1 GLOSSARY OF TERMS

**Loss limit** As per Compliance: maximum amount a Player can loose in monetary value of their deposits.

**Bet limit** As per Compliance: maximum value a Player can wager/bet

**Loss Limit Period** Period during which the player can lose.

**Balance** Funds in the players cash balance, available for wagering or cashin.

**Purchase (Deposit)** Money transferred from the players personal bank account into the casino.

**Cashin request** When the Player clicks on the withdraw button in the Lobby

**Reversible Period** Player has 24 - 72hrs to reverse their cashin.

**Flush** When the Payments team starts to process the payment. This is when the money leaves the Players balance and they are unable to access it. This is also when the amount the player has available to lose is adjusted.

**Review Period** The money goes to into a workflow and can spend up to a week here (request docs etc) Player can request some money back (Cash Against Withdrawal) and money is sent back to Players account, realised through an admin event. This has no effect on the loss limit. Cash against withdrawals will not be allowed.

**Processed** Payment is flushed at 1pm, and goes to the payment methods. The money leaves DOS bank account. Takes 3-7 days.

**Import** The recon file is uploaded to the back office and the payment goes to 'paid' status in the back office.

**Credit Against Withdrawal (CAW) / Reversal / Refund User Token** These all mean the same things.

**Wager / Bet (Income)** Value of the bet placed and income generated.

**Payout** Value of the outcome of the bet placed.

**NGR** Wager – payout = NGR (excludes wagering from bonus money)

**Cumulative NGR for Period** NGR summed for the period

**Cumulative NGR for Player** NGR summed for the players since they started playing with us

**Remaining Loss limit** Balance of the player set loss limit available for the player still to lose in a given period.

**Wins Carry over periods (Payouts In Play)** Limit available for the player to lose, that are carried over from one period to the next, where those limits were accumulated from payouts greater than the players set loss limit in the previous period.

**Total available loss limit** Total loss limit available to the user in given period; includes loss limits from the player set loss limits and loss limits from wins carry over period.

## Legislation

Gaming Regulations Art 87

1 From the opening of the player account the player must, at all times, have easy access to the following information on their gaming activity during a specific time period:

   a. bets;  
   b. winnings;  
   c. net result of the gaming activity.

2 From the opening of the player account the organiser will demand that the player set one or more maximum amounts they wish to limit their daily, weekly or monthly bets or losses to.

4 The player must be able to adjust the maximum amount they have set at any time. Lowering a maximum amount will be effective immediately. Increases will be effective after 24 hours at the earliest.

## Switzerland Loss Limits

This document pertains to the requirements for the Switzerland loss limit system and related calculations. It includes the business rules and requirements from DOS.

Sign-off by DOS

DOS agreed to the contents of this document on the 27th of March 2020.

## Business Rules

All the DOS business rules have been moved to the relevant sections where they are addressed.  
The table below is for easy reference.

### TABLE 2 DOS BUSINESS RULES

| ID | Details | Section |
|---|---|---|
| BR.1 | Loss limits must be calculated against Cash money only, not Bonus money. | Core Functionality |
| BR.2 | Loss limits for the period (daily/weekly/monthly) must be reset at midnight on the Gaming Server's time, not the Players midnight. | Reset of loss limit. |
| BR.3 | When a Player's bet is larger than the remaining loss limit then the bet must be prevented from being made and a notification shown to the Player. | Core Functionality Lobby |
| BR.4 | When a Player receives cash winnings, the cash winnings amount must be added to the remaining loss limit amount. | Core Functionality |
| BR.5 | When a Player's loss limits are due reset at midnight for the new period and the available loss limit for the old period is greater than the amount that the Player set, then the previous limit must be carried over into the next period. | Tracked Value/Usage |
| BR.6 | When a Player's loss limits are due to reset at midnight for the new period and the tracked value is loss limit for the old period is less than the amount that the Player set, then the limit must be reset. | Tracked Value/Usage |
| BR.7 | When a Player cashes in their full cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the loss limit must be reset. | Tracked Value/Usage |
| BR.8 | When a Player cashes in a portion of their cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the partial cashin amount must be deducted from the remaining loss limit. If the partial amount is greater than the payouts in play, then effectively this cancels the payouts in play and the original loss limit is re-instated. | Tracked Value/Usage |
| BR.10 | When a Player increases their loss limit, the increase increment must be added to the original amount after 24 hours. | Setting Loss limits |
| BR.11 | When a Player decreases their loss limit for a period, the decrease increment must be removed from the original amount immediately. | Setting Loss limits |
| BR.12 | When a Player's loss limit for the period is reset after a full cashin (see BR.7) however a full refund is made to the Player, the previous remaining loss limit must be re-instated. | Tracked Value/Usage |
| BR.13 | When a Players Bonus balance is converted to Cash balance, the loss limit must be increased by the same value. | Bonus to cash – Playthrough. |
| BR.14 | When a Player cashes in their full or portion of their cash balance, and the cashin is flushed, and the remaining loss limit is lower than the set loss limit (there are no payouts in play), the loss limit must remain untouched. | Bonus to cash – Playthrough. |
| BR.15 | When a Player forfeits or re-instates their bonus, it should not affect their Loss limit. | No reference |
| Req.1 | Implement a feature to allow a host to view the loss limits that the Player set: Daily/Weekly/Monthly. | RG API Back Office |
| Req.2 | Implement a feature to allow a host to view the remaining loss limit for the period for the Player: Daily/Weekly/Monthly. | RG API Back Office |
| Req.3 | Implement a feature to allow a Customer Care Agent to edit the loss limits for the Player: Daily/Weekly/Monthly. | RG API Back Office |
| Req.4 | Implement a message for a host when loss limit validation does not pass. | Back Office |
| Req.5 | Implement a message for a host for when a player has a pending limit increase and they request to change their limits, advising of the pending change along with the date it was actioned. | RG API Back Office |
| Req.6 | Implement a feature to allow a host to cancel the pending increase for a Player. | RG API Back Office |
| Req.7 | Record the details when a loss limit is set or updated: 1. Who changed the limit. 2. Where the limit was changed (RG, API, Backoffice). 3. What the limit was before it changed. 4. What the limit was changed to. 5. When the limit was changed | Back Office |
| Req.8 | When a loss limit is breached, the system must alert the Business. | Event on limit reached |
| Req.9 | When a Player has a Provisional status but has a loss limit set that is greater than CHF1000, the system must alert the Business. | No |
| Req.10 | Transactional logs must be kept to record the Player's loss limit progression. The logs must contain the following data – detailed in the link | No log Back Office |
| Req.12 | Implement a message for a Player when the loss limit is reached and the bet is prevented from being made. | As per BR 3 |

## Core Functionality

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.1 | Loss limits must be calculated against Cash money only, not Bonus money. | The core functionality of loss limits works around tracking of wagers and wins of individual players and comparing that tracked value against loss limits set by the player. Only cash is considered for loss limit calculations. In the case of a BCR split on a wager only the cash portion would affect the loss limit tracking. When the player places a wager, the sum of the value of the wager and the tracked value is compared against the loss limits (all three periods) of the player. If that sum is less than or equal to the loss limits the wager is allowed: wager value + tracked value <= Loss limits If that sum would exceed any one of the loss limits the wager is blocked: wager value + tracked value > Loss limits | This is done in the background and is current functionality. | Agreed |
| BR.2 | Loss limits for the period (daily/weekly/monthly) must be reset at midnight on the Gaming Server's time, not the Players midnight. | The individual loss limit tracking values are only reset if there are no “wins in play” for the period. The resets are all calendar based and all times are gaming server time. Daily reset on 24:00 UTC every night. Weekly resets on 24:00 UTC if the new day is a Monday. Monthly resets on 24:00 UTC if the new day is the 1st day of any month. | This is done in the background and is current functionality. | Agreed |
| BR.3 | When a Player's bet is larger than the remaining loss limit then the bet must be prevented from being made and a notification shown to the Player. | If that sum is less than or equal to the loss limits the wager is allowed: wager value + tracked value <= Loss limits If that sum would exceed any one of the loss limits the wager is blocked: wager value + tracked value > Loss limits | This is done in the background and is current functionality. | Agreed |
| BR.4 | When a Player receives cash winnings, the cash winnings amount must be added to the remaining loss limit amount. | The core functionality of loss limits works around tracking of wagers and wins of individual players and comparing that tracked value against loss limits set by the player. Only cash is considered for loss limit calculations. | This is done in the background and is current functionality. | Agreed |

### FIGURE 1 CORE FUNCTIONALITY REQUIREMENTS AND CURRENT FUNCTIONALITY

The core functionality of loss limits works around tracking of wagers and wins of individual players and comparing that tracked value against loss limits set by the player. Only cash is considered for loss limit calculations. In the case of a BCR split on a wager only the cash portion would affect the loss limit tracking. When the player places a wager, the sum of the value of the wager and the tracked value is compared against the loss limits (all three periods) of the player.

If that sum is less than or equal to the loss limits the wager is allowed:  
wager value + tracked value <= Loss limits

If that sum would exceed any one of the loss limits the wager is blocked:  
wager value + tracked value > Loss limits

### Setting Loss limits

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.10 | When a Player increases their loss limit, the increase increment must be added to the original amount after 24 hours. | Loss limit is increased after 24 hours. | This is done in the background and the information can be retrieved via the RG API. This is existing functionality. | Agreed |
| BR.11 | When a Player decreases their loss limit for a period, the decrease increment must be removed from the original amount immediately. | Decrease is immediate | This is done in the background and the information can be retrieved via the RG API. This is existing functionality. | Agreed |

### FIGURE 2 SETTING LOSS LIMITS REQUIREMENTS AND CURRENT FUNCTIONALITY

Loss limits can be set or updated by the player in the Responsible Gaming Application. The player is forced to set at least one limit during the registration process. 3 different loss limits can be set based on time periods: daily, weekly and monthly.

When loss limits are updated to be less restrictive than the current loss limits a cooling off period takes effect. These values are placed into a pending state and is only applied when the cooling off period is over (24 hours in Switzerland) – so if set at 2pm will be effective at 2pm next day (24 hours later). For example:

### TABLE 3 SETTING LOSS LIMITS EXAMPLE

| New Loss Limit | Current Loss Limit | Cooling off period applied |
|---|---|---|
| 200 | 1000 | No |
| 1000 | 200 | Yes |
| 0 | 1000 | Yes, since 0 represents unlimited |

Pending limits are applied at two different points in the system. Before a player performs a wager and when the loss limits details are fetched from the relevant API.

### Tracked Value/Usage

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.5 | When a Player's loss limits are due reset at midnight for the new period and the available loss limit for the old period is greater than the amount that the Player set, then the previous limit must be carried over into the next period. | Tracking for loss limits happens in one column per period per player. A negative value indicates “wins in play”. | This is done in the background and is current functionality. | Agreed |
| BR.6 | When a Player's loss limits are due to reset at midnight for the new period and the tracked value is loss limit for the old period is less than the amount that the Player set, then the limit must be reset. |  | This is done in the background and is current functionality. | Agreed |
| BR.7 | When a Player cashes in their full cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the loss limit must be reset. |  | This is done in the background and is current functionality. | Agreed |
| BR.8 | When a Player cashes in a portion of their cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the partial cashin amount must be deducted from the remaining loss limit. If the partial amount is greater than the payouts in play, then effectively this cancels the payouts in play and the original loss limit is re-instated. |  | This is done in the background and is current functionality. | Agreed |
| BR.12 | When a Player's loss limit for the period is reset after a full cashin (see BR.7) however a full refund is made to the Player, the previous remaining loss limit must be re-instated. | As above | This is done in the background and is current functionality. | Agreed |

### FIGURE 3 TRACKED VALUE REQUIREMENTS AND CURRENT FUNCTIONALITY

Tracking for loss limits happens in one column per period per player. A negative value indicates “wins in play”. For example:

### TABLE 4 TRACKED VALUE EXAMPLE

| Loss Limit | Tracked Value/Usage | Total Loss Limit Available |
|---|---|---|
| 1000 | 990 | 10 |
| 1000 | -1500 | 2500 |
| 1000 | 1000 | 0 |

### Reset of loss limit.

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.2 | Loss limits for the period (daily/weekly/monthly) must be reset at midnight on the Gaming Server's time, not the Players midnight. | The individual loss limit tracking values are only reset if there are no “wins in play” for the period. The resets are all calendar based and all times are gaming server time. Daily reset on 24:00 UTC every night. Weekly resets on 24:00 UTC if the new day is a Monday. Monthly resets on 24:00 UTC if the new day is the 1st day of any month. | Build into RG API. This is current functionality. | Agreed |

### FIGURE 4 RESET LOSS LIMIT REQUIREMENT AND CURRENT FUNCTIONALITY

The individual loss limit tracking values are only reset if there are no “wins in play” for the period. The resets are all calendar based and all times are gaming server time.

Daily reset on 24:00 UTC every night.  
Weekly resets on 24:00 UTC if the new day is a Monday.  
Monthly resets on 24:00 UTC if the new day is the 1st day of any month.

### Core Test Cases

Refer to Appendix A

## BONUS TO CASH – PLAYTHROUGH

### Bonus to cash – Playthrough.

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.13 | When a Players Bonus balance is converted to Cash balance, the loss limit must be increased by the same value. | Bonus flushed to cash is considered winnings from a loss limit standpoint. Thus, any bonus to cash conversion is subtracted from the loss limit usage/tracked value | This is current functionality that takes place in the background. | Agreed |
| BR.14 | When a Player cashes in their full or portion of their cash balance, and the cashin is flushed, and the remaining loss limit is lower than the set loss limit (there are no payouts in play), the loss limit must remain untouched. |  | This is current functionality that takes place in the background. | Agreed |

### FIGURE 5 BONUS TO CASH REQUIREMENT AND CURRENT FUNCTIONALITY

Bonus flushed to cash is considered winnings from a loss limit standpoint. Thus, any bonus to cash conversion is subtracted from the loss limit usage/tracked value. For example:

### TABLE 5 PLAYTHROUGH EXAMPLE

| Loss Limit | Tracked Value/Usage Before Flush | Flush Amount | Tracked Value/Usage After Flush |
|---|---|---|---|
| 1500 | 200 | 1000 | -800 |
| 1000 | -1500 | 1000 | -1500 |

### Bonus Flush Test Cases

To be added to Appendix A.

## Withdrawals/Cashins

This is the new requirement where we will reset the loss limit when the cashin has been flushed.

| ID | New development | Derivco New Functionality | Ho to achieve | Agreement required |
|---|---|---|---|---|
| Derivco ID 1 | The loss limit will be reset on flushed cashin. | When the player’s cashin in flushed, the amount exposed is reduced by the amount flushed. | Derivco will do development to reset the loss limit on flushed cashin. | Agreed |

### FIGURE 6 LOSS LIMIT RESET

### FIGURE 7 RESET LOSS LIMIT ON FLUSHED CASHIN

Cashin process flow

### TABLE 6 CASHIN PROCESS FLOW

### CAWs/User Refund Tokens – To be confirmed by DOS

DOS has decided, from a business perspective, that no CAWs, user refund tokens or the like will be done in Switzerland. This in turn means that it is not a requirement that the loss limit system caters for these refunds.

The 3 scenarios where withdrawal refunds are used and how it will be compensated for:

- Fraud – if during the review period an account is marked as fraudulent the account is closed and the withdrawal reversed. In this case, since the account is closed it would not matter if we adjust the loss limits as the player can no longer play.
- Failed payment (incorrect account) – Instead of pushing the funds back into the account by default the player will be contacted to get the correct account details. If this is not possible and the amount is refunded to the Casino account, it will not affect the loss limit.
- Player wants it reversed - DOS will not allow this. If this happens, it will be reversed and it will not affect the loss limit.

### Mistakenly flushed

There may be scenarios in which a withdrawal is mistakenly flushed and CAW’d back to the player, resulting in the loss limit not being adjusted. An extreme example:

A player hits a jackpot and wins 2,000,000 Swiss Franc which he withdraws. Wins of this magnitude is paid out at a reduced rate based on available funds, cashflow etc. For this example, let’s say 20,000 a day. If by accident the entire withdrawal is flushed at once the loss limits will be adjusted for the full amount. Since that amount cannot be paid out it will be rolled back but the loss limit system does not cater for the reversal.

Since this would be a rare edge case, one option is for the operator to contact Derivco and ask for the loss limit usage to be adjusted accordingly.

### Withdrawals Test Cases

Refer to Appendix A

## Generated Events

These are Event Insight events.

### Event on limit set

Setting of loss limits generates an EI event indicating the new set values.

### Event on limit reached

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | Dos Requirement | Derivco Current Functionality | Ho to achieve | Agreement required |
|---|---|---|---|---|
| Req.8 | When a loss limit is breached, the system must alert the Business. | An even is triggered when the loss limit is reached. | An event is sent to DOS. This is current functionality. | Agreed |

### FIGURE 8 EVENT INSIGHT REQUIREMENT AND FUNCTIONALITY

An EI event is generated whenever a wager would exceed any of the three loss limits. If the wager size is decreased and it would not exceed a loss limit it will continue gameplay as per normal.

In the below example the player “reached” his limit twice but decreased his wager size to continue playing. The last two times the player’s limit was reached the player was on his limit and decreasing wager size would make no difference.

### TABLE 7 EXAMPLE OF EVENT ON LIMIT REACHED

| Loss Limit | Usage | Wager Size | Win | Limit Reached Event |
|---|---|---|---|---|
| 15.00 | 0 | 5.00 | 0 | No |
| 15.00 | 5.00 | 10.00 | 7.00 | No |
| 15.00 | 8.00 | 10.00 | - | Yes |
| 15.00 | 8.00 | 5.00 | 0 | No |
| 15.00 | 13.00 | 5.00 | - | Yes |
| 15.00 | 13.00 | 2.00 | 4.00 | No |
| 15.00 | 11.00 | 2.00 | 0 | No |
| 15.00 | 13.00 | 2.00 | 0 | No |
| 15.00 | 15.00 | 2.00 | - | Yes |
| 15.00 | 15.00 | 1.00 | - | Yes |

## Responsible Gaming

### Player Message

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to Achieve | Agreement required |
|---|---|---|---|---|
| BR.3 | When a Player's bet is larger than the remaining loss limit then the bet must be prevented from being made and a notification shown to the Player. | When a player reached his loss limit then a message must be displayed informing the player that the loss limit has been reached for the relevant period. After the message is displayed, the player will need to adjust their bet. Currently the game session is closed when the loss limit is reached. | Veyron triggers a message. This is current functionality. | Agreed |

### FIGURE 9 PLAYER ALERT REQUIREMENT AND CURRENT FUNCTIONALITY

When a player reached his loss limit then a message must be displayed informing the player that the loss limit has been reached for the relevant period. After the message is displayed, the player will need to adjust their bet. Currently the game session is closed when the loss limit is reached.

### Loss limit information

An explanation of how loss limits work should be available to the player in the terms and conditions or within the responsible gaming application.

## Back Office

The table below refers to the DOS requirement and the functionality offered by Derivco. The purpose of this presentation that we can see at a glance what is required and what is offered.

| ID | DOS Requirement | Derivco Current Functionality | How to achieve | Agreement Required |
|---|---|---|---|---|
| Req.1 | Implement a feature to allow a host to view the loss limits that the Player set: Daily/Weekly/Monthly. | Use the RG API to retrieve this information. It is not available in the Derivco back office. and show to the player in another application | This information is currently available via the RG API. DOS will need to display this via their own application. | Agreed |
| Req.2 | Implement a feature to allow a host to view the remaining loss limit for the period for the Player: Daily/Weekly/Monthly. | Use the RG API to retrieve this information. It is not available in the Derivco back office. and show to the player in another application | Use the RG API to retrieve this information. It is not available in the Derivco back office. and show to the player in another application | Agreed |
| Req.3 | Implement a feature to allow a Customer Care Agent to edit the loss limits for the Player: Daily/Weekly/Monthly. | This information is currently available via the RG API. DOS will need to display this via their own application. | This information is currently available via the RG API. DOS will need to display this via their own application. | Agreed |
| Req.4 | Implement a message for a host when loss limit validation does not pass. | Not available | N/A | Agreed |
| Req.5 | Implement a message for a host for when a player has a pending limit increase and they request to change their limits, advising of the pending change along with the date it was actioned. | Not Available | N/A | Agreed |
| Req.6 | Implement a feature to allow a host to cancel the pending increase for a Player. | Not available | N/A | Agreed |
| Req.7 | Record the details when a loss limit is set or updated: 1. Who changed the limit. 2. Where the limit was changed (RG, API, Backoffice). 3. What the limit was before it changed. 4. What the limit was changed to. 5. When the limit was changed | We have the following information available: Player Account Loss Limit change date Changed by Operator or Player Change App – Account API, RGAPI Previous Limit New Limit Limit type Pending – yes Effective date and time | Information available on PTS. DOS to access this from the PTS. | Agreed |
| Req.8 | When a loss limit is breached, the system must alert the Business. | Event alerts business. | Current functionality available via Event Insight. | Agreed |
| Req.9 | When a Player has a Provisional status but has a loss limit set that is greater than CHF1000, the system must alert the Business. | Provisional player can only deposit CHF 1000. | Not available. | Agreed |
| Req.10 | Transactional logs must be kept to record the Player's loss limit progression. The logs must contain the following data – detailed in the link Player ID Loss Limit Period - Remaining loss limit amountDaily - Weekly - Monthly Balance Purchase Cashin Wager / Bet Payout NGR Cumulative NGR for Period (not for Phase 1) Cumulative NGR for Player (not for Phase 1) Total available loss limit | We have the following information available: Player ID Loss Limit Period Remaining Loss limit period Balance | There is a transactional log for all of loss limits, not for certain fields. | Agreed |

### FIGURE 10 BACKOFFICE REQUIREMENTS AND CURRENT FUNCTIONALITY

## Appendix A – test Cases

We are still in the process of completing the test cases.

### TABLE 8 DERIVCO TEST CASES

| Given | When | Then |
|---|---|---|
| A player with no limits | the player sets a daily limit only | a daily limit is set and is applied immediately |
| A player with no limits | the player sets a weekly limit only | a weekly limit is set and is applied immediately |
| A player with no limits | the player sets a monthly limit only | a monthly limit is set and is applied immediately |
| A player with no limits | the player sets a daily and weekly limit only | a daily and weekly limit is set and is applied immediately |
| A player with no limits | the player sets a daily and monthly limit only | a daily and monthly limit is set and is applied immediately |
| A player with no limits | the player sets a weekly and monthly limit only | a weekly and monthly limit is set and is applied immediately |
| A player with no limits | the player sets a daily, weekly and monthly limit | a daily, weekly and monthly limit is set and is applied immediately |
| A player with a daily limit | the player sets a weekly limit | the players daily limit remains unchanged and a weekly limit is set and is applied immediately |
| A player with a daily limit | the player sets a monthly limit | the players daily limit remains unchanged and a monthly limit is set and is applied immediately |
| A player with a weekly limit | the player sets a daily limit | the players weekly limit remains unchanged and a daily limit is set and is applied immediately |
| A player with a weekly limit | the player sets a monthly limit | the players weekly limit remains unchanged and a monthly limit is set and is applied immediately |
| A player with a monthly limit | the player sets a daily limit | the players monthly limit remains unchanged and a daily limit is set and is applied immediately |
| A player with a monthly limit | the player sets a weekly limit | the players monthly limit remains unchanged and a weekly limit is set and is applied immediately |
| A player with a daily and weekly limit | the player sets a monthly limit | the players daily and weekly limits remain unchanged and a monthly limit is set and is applied immediately |
| A player with a daily and monthly limit | the player sets a weekly limit | the players daily and monthly limits remain unchanged and a weekly limit is set and is applied immediately |
| A player with a weekly and monthly limit | the player sets a daily limit | the players weekly and monthly limits remain unchanged and a daily limit is set and is applied immediately |
| A player with a daily, weekly and monthly limit | the player decreases the daily limit | the players weekly and monthly limits remain unchanged and the daily limit is set and is applied immediately |
| A player with a daily, weekly and monthly limit | the player decreases the weekly limit | the players daily and monthly limits remain unchanged and the weekly limit is set and is applied immediately |
| A player with a daily, weekly and monthly limit | the player decreases the monthly limit | the players daily and weekly limits remain unchanged and the monthly limit is set and applied immediately |
| A player with a daily, weekly and monthly limit | The player increases the daily limit | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending daily limit is set |
| A player with a daily, weekly and monthly limit | The player increases the weekly limit | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending weekly limit is set |
| A player with a daily, weekly and monthly limit | The player increases the monthly limit | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending monthly limit is set |
| A player with a daily, weekly and monthly limit | the player sets the daily limit to unlimited | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending daily limit is set |
| A player with a daily, weekly and monthly limit | the player sets the weekly limit to unlimited | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending weekly limit is set |
| A player with a daily, weekly and monthly limit | the player sets the monthly limit to unlimited | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending monthly limit is set |
| A player with a daily, weekly and monthly limit | The player increases the daily limit and then decreases the daily limit to below the original amount | the players weekly and monthly limits remain unchanged and the daily limit is set and is applied immediately |
| A player with a daily, weekly and monthly limit | The player increases the weekly limit and then decreases the weekly limit to between the original and previous amounts | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending weekly limit is set |
| A player with a daily, weekly and monthly limit | The player increases the monthly limit and then increases the monthly limit higher than the previous amount | the players daily, weekly and monthly limits remain unchanged and a 24 hour pending monthly limit is set |
| A player with a daily, weekly and monthly limit | The player decreases the daily limit and then increases the daily limit to between the original and decreased limits | the players weekly and monthly limits remain unchanged and the daily limit is set to the decreased amount and applied immediately and a 24 hour pending daily limit is set for the higher amount |
| A player with a daily, weekly and monthly limit | The player decreases the weekly limit and then decreases the weekly limit | the players daily and monthly limits remain unchanged and the weekly limit is set to the last decreased amount and applied immediately |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager for an amount less than their limits | the wager is accepted |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager for an amount exactly equal to their daily limit | the wager is accepted |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager for an amount exactly equal to their weekly limit | the wager is accepted |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager for an amount exactly equal to their monthly limit | the wager is accepted |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager higher than their daily limit | the wager is not accepted and the player receives a daily loss limited exceeded error message |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager higher than their weekly limit | the wager is not accepted and the player receives a weekly loss limited exceeded error message |
| A player with a daily, weekly and monthly limit | the player attempts to place a wager higher than their monthly limit | the wager is not accepted and the player receives a monthly loss limited exceeded error message |
| A player with a daily, weekly and monthly limit and gameplay which has resulted in a Player loss | The player decreases the daily limit to an amount higher than their current daily losses and places a wager | the players daily limit is set and applied immediately and the player receives a daily loss limit exceeded error message |

## Appendix B – DOS Use Cases

| ID | Business Rule | User Acceptance Criteria |
|---|---|---|
| BR.3 | When a Player's bet is larger than the remaining loss limit then the bet must be prevented from being made and a notification shown to the Player. | Preconditions: - Player has set one or more limits - Player remaining loss limit for the period: $10 - Player has $20 in cash balance Test 1: Input: - Player places a bet of $11 Output: - Player should not be able to make the bet. - Player should be shown the two notifications in-game. Why: Because his $11 bet could lose however he only has $10 left to lose for the period. |
| BR.4 | When a Player receives cash winnings, the cash winnings amount must be added to the remaining loss limit amount. Note: The winnings amount must be added to each of the deposit limit values that were set (daily/weekly/monthly) | Preconditions: Player has set one or more limits. Player remaining loss limit for the period: $10 Player has $20 in cash balance Test 1: Input: - Player places a bet of $5 - Player has a payout of $12 of cash money - Player has a $27 cash balance. Output: - Players new loss limit for the period should be: $17 o $7 should be added to the daily, weekly, and monthly (if set) Why: $10 (the remaining loss limit for the period) plus $7 (NGR: -$5 (wager) + $12 (winnings)) = $17 |
| BR.5 | When a Player's loss limits are due reset at midnight for the new period and the available loss limit for the old period is greater than the amount that the Player set, then the previous limit must be carried over into the next period. | Preconditions: Player has set one or more limits. Player set a loss limit: $10 Player has $20 in cash balance Test 1: Input: - Player places a bet of $5 - Player has a payout of $20 of cash money. - Player loss limit for the period is now $15 (10 set loss limit – 5 wager + 20 winnings) - Player places no more wagers for the day. - Player logs in the next day. Output: - Players new loss limit for the period should be: $15 - If the period being reset is the daily limit, then this should not affect the weekly or monthly limit. - If the period being reset is the weekly limit, then this should not affect the monthly limit. Why: $15 (the remaining loss limit for the old period) = higher than the set daily loss limit of $10, therefore the limit must be carried over into the new period. |
| BR.7 | When a Player cashes in their full cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the loss limit must be reset. Note: Flushed = this when the cashin status is moved from Requested to Flushed in the backoffice. See BR.14 for what happens when a Players loss limit is lower than what they set. As per a meeting on 2020-02-26 - there is no difference between a Manual or Auto flush. Confirmed no difference. | Preconditions: Player has set one or more limits. Player set a loss limit: $10 Player has $20 in cash balance Test 1: Input: - Player places a bet of $5 - Player has a payout of $12 of cash money - Player has a $27 cash balance - Player has a $17 remaining loss limit - Player does a full cash withdrawal - Players money is flushed Output: - Players cash balance is $0 - Players new loss limit should be: $10 - The reset must be applied to any period: daily, weekly or monthly Why: $17 (the remaining loss limit for the period) is greater $10 (Player set daily limit), therefore it must be reset. |
| BR.8 | When a Player cashes in a portion of their cash balance, and the cashin is flushed, and the remaining loss limit is higher than the set loss limit (there are payouts in play), the partial cashin amount must be deducted from the remaining loss limit. If the partial amount is greater than the payouts in play, then effectively this cancels the payouts in play and the original loss limit is re-instated. | Preconditions: Player has set one or more limits. Player remaining loss limit for the period: $10 Player has $20 in cash balance Test 1: Input: - Player places a bet of $5 - Player has a payout of $12 of cash money - Player has a $27 cash balance. - Player does a $2 cash withdrawal - Players money is flushed Output: - Players cash balance is $25 - Players new loss limit for the period should be: $15 Why: $10 (the remaining loss limit for the period) + $7 (NGR: -$5 (wager) + $12 (winnings)) - $2 (withdrawal) = $15. |
| BR.10 | When a Player increases their loss limit, the increase increment must be added to the original amount after 24 hours. | Preconditions: Player set a daily loss limit: $10 Player remaining loss limit for the period: $120 Test 1: Input: - Player increases their daily loss limit to $20 Output: - Players loss limit for the period should remain at $120 for the next 24hrs. - After 24hrs the Players new loss limit should be $130 |
| BR.11 | When a Player decreases their loss limit for a period, the decrease increment must be removed from the original amount immediately. | Preconditions: Player set a daily loss limit: $20 Player remaining loss limit for the period: $100 Test 1: Input: - Player decreases their daily loss limit to $10 Output: - Players loss limit for the period should be $90 o The must be applied to any period: daily, weekly or monthly |
| BR.13 | When a Players Bonus balance is converted to Cash balance, the loss limit must be increased by the same value. | Preconditions: Player set a daily loss limit: $20 Player remaining loss limit for the period: $30 Player has $50 cash balance and a $10 bonus balance Test 1: Input: - Player meets their bonus wagering requirements at that stage and their bonus is converted to Cash. Output: - Players cash balance should be $60 - Players bonus balance should be $0 - Players loss limit for the period should be $40 |
| BR.14 | When a Player cashes in their full or portion of their cash balance, and the cashin is flushed, and the remaining loss limit is lower than the set loss limit (there are no payouts in play), the loss limit must remain untouched. | Preconditions: Player has set one or more limits. Player set a loss limit: $10 Player has $20 in cash balance Test 1: Input: - Player places a bet of $5 - Player has a payout of $3 of cash money - Player has a $18 cash balance. - Player has a $8 remaining loss limit - Player does a partial cashin. - Players money is flushed Output: - Players new loss limit for the period should be: $8 Why: $10 (the remaining loss limit for the period) + $-2 (NGR: -$5 (wager) + $3 (winnings)) = less than the set daily loss limit of $10, therefore the remaining loss limit must remain untouched. |