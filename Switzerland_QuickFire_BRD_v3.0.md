---
country: Switzerland
document_name: Switzerland QuickFire Solution
source_file: Switzerland QuickFire BRD v3.0.pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# Switzerland QuickFire Solution

**Analyst:** Ashley Dhunraj  
**Department:** Quickfire - Business Analyst  
**Version:** 3.0  
**Release Date:** 02/04/2020  
**Project:** Switzerland QuickFire Solution  
**MGS Order No.:** TBD

## Table of Contents

- Table of Contents
- Revision History
- Introduction
- Scope
- Out of Scope
- Teams Impacted
- Casino
- Other
- Products In Scope
- Business Requirements

## Revision History

| Revision | Date | Changed By | Comments / Reason |
|---|---|---|---|
| 1.0 | 20 Feb 2019 | Ashley Dhunraj | Initial Version |
| 1.1 | 22 Feb 2019 | Ashley Dhunraj | Added notes to sections 1.3.3 and 1.7 |
| 1.2 | 25 Feb 2019 | Ashley Dhunraj | Updated the note on section 1.7 |
| 1.3 | 16 July 2019 | Ashley Dhunraj | Updated notes, Teams Impacted and section 1: Games |
| 2.0 | 27 March 2020 | Ashley Dhunraj | Added section 4. Updated section 1.7 |
| 3.0 | 02 April 2020 | Ashley Dhunraj | Struckthrough section 1.7 – Applicable to Sportsbook only |

## Introduction

This document provides the business requirements for Switzerland where we are looking to have games introduced into the regulated marked space. The requirements are based on the regulations specified by the regulatory body of Switzerland.

This document will also highlight the adoption of the gaming components that will be customized to suit the Swiss regulated market.

As a reference, Switzerland legislation documents can be found at the following location:  
Switzerland Legislation

## Scope

As with most Quickfire solutions, the bulk of the work will be pushed to the operator. However, we are still responsible for the gaming content. This includes translations, currency support and bet settings, as well as unique market requirements detailed in the business requirement section below.

The following games are in scope:

1. Slot Games
2. Table Games

## Out of Scope

The following are out of scope.

1. Multiplayer games
2. Live Games (Live Dealer)
3. Jackpots / Progressives - (No shared liquidity in Switzerland)

The below checklists have been completed based on the information gathered to date and are merely intended to be an indication of the identified scope thus far. Both the BA and the relevant developers will be responsible for maintaining it for the duration of the project.

## Teams Impacted

### Casino

### Other

## Products In Scope

| Product / Area | In Scope |
|---|---|
| Viper Core | X |
| Feature Rich Games | X |
| Build & Configure MPV |  |
| Flash Core | X |
| Integrations Support |  |
| Casino DB |  |
| Web Tech |  |
| Casino Config |  |
| Land Based |  |
| White Box Testing |  |
| HTML5 – Lobby Tools Dev |  |
| QA Dev Partners |  |
| HTML5 - Games | X |
| Live Dealer Services |  |
| Casino Architecture |  |
| HTML5 - Core | X |
| Casino Architecture |  |
| Markets |  |
| Mobile Download |  |
| Form Service |  |
| Bingo |  |
| Poker |  |
| Banking |  |
| Registration |  |
| PCM |  |
| Testing | X |
| Usability |  |
| Art |  |
| Playability |  |
| End Process QA | X |
| Back Office |  |
| Service Managers | X |
| IT |  |
| Viper HTML5 Lobby |  |
| iCafe / On Cash |  |
| CiP |  |
| Flash (Lobby) |  |
| HTML5 Instant Play |  |
| Sportsbook |  |
| CiB |  |
| Flash Instant Play |  |
| Land Based MPV |  |
| MPF |  |
| Quickfire | X |
| Live Dealer |  |
| My Account |  |
| PlayCheck | X |
| Forgot Password |  |
| Responsible Gaming |  |
| Help (Flare) |  |
| Loyalty |  |
| Change Username |  |
| Avatar |  |
| NemID Login App |  |
| Open Bets Redirector |  |
| Change Password |  |
| Alias Activation |  |
| CAPI |  |
| Integrity Checker |  |
| Change Contact Details |  |
| H5 QuickFire | X |

## Business Requirements

### 1. Games

#### 1.1. Currency

##### 1.1.1.

The Swiss franc and Euro will be the only supported currency.

#### 1.2. Language

##### 1.2.1.

There are no specific language requirements in the legislation. The legislation mentions “… must be in easily understandable language”.

The certification protocol document however mentions:

- The language used for reporting and communication purposes will be English,
- that technical documentation coming from the applicant may be in any of the official Swiss languages or English.

Note: The understanding is that discussions with Swiss operators will determine what languages are used. The casino languages supported will be German, English, French, Italian.

#### 1.3. Access to Help

##### 1.3.1.

Microgaming game help files must be available in English for all Microgaming casino games.

##### 1.3.2.

Translated versions of helpfiles must be made available in official Swiss languages (German, French and Italian)

##### 1.3.3.

Help files must be approved by the regulator prior to going live.

#### 1.4. RTP

##### 1.4.1.

The RTP must be displayed in help files.

##### 1.4.2.

All casino games must have a theoretic pay-out ratio of at least 80 per cent, but a maximum of 100 per cent.

#### 1.5. Wager Cycle

##### 1.5.1.

Quickspin can be enabled for all Swiss casinos, as no minimum time for each spin is mentioned.

#### 1.6. Autoplay

##### 1.6.1.

Where an automatic replay of the game is triggered the player must be able to end the game after the current game unit (i.e. the player must be given the option stop Autoplay at after each spin)

#### 1.7. Free Games

##### 1.7.1.

Free games are permitted. This should be added with any op that is tested for Switzerland.

##### 1.7.2.

A separate account for free games must be used.

##### 1.7.3.

Free games do not constitute part of the gross gaming revenue.

Note: The testing needs to ensure that the operator is providing separate naming conventions (under 17 characters) for a player being awarded freegames vs normal gameplay.  
E.g. if player A is given freegame they need to prefix with 1_A and normal account is A (both exclude our prefix).  
The requirements state that the account needs to be separated and on top be easily distinguished as they are taxed.  
Further the op will need to have summarised payouts enabled to allow the extended elements  
If free games in our reports are grouped in the GGR, so we would need to split this out. We currently do not have separate accounts for Free Games and Cash Balance (i.e. we would need multiple player accounts)  
The above requirements, as confirmed by compliance, is applicable to Sportsbook only - not Casino.

#### 1.8. Player Limit

##### 1.8.1.

The maximum number of players participating in the same casino game is limited to 1000. This maximum number does not apply to jackpot systems

Note: This requirement does not apply to slot games, as per the certification protocol document.  
Regarding automated money games, this requirement has in principal no relevance, as the decision of the game (i.e. a RNG-number) is unique for each game and each player.  
Regarding live table games, the decision of the game (i.e. the roulette number) is normally used for more than one player. Therefore, the access to the same game must be limited to 1000 players by the platform.

### 2. Playcheck

#### 2.1.

From the opening of the player account the player must, at all times, have easy access to the following information on their gaming activity during a specific time period:

- bets;
- winnings;
- net result of the gaming activity.

#### 2.2.

All events and the results of the game, as well as all other information of the current game and at least of the four previous ones must be registered.

#### 2.3.

The last 50 free games must be displayed – Landbased requirement

### 3. Certification

#### 3.1.

Full certification of the Gaming System will be required to be completed before an Operator can go live.

#### 3.2.

Games must be certified.

#### 3.3.

The gaming house (operator) may only purchase online games from suppliers who is ISO/IEC 27001:2013 certified.

Note: MGS has confirmed a solution is in place for the ISO certification requirement for Quickfire, that should allow us to move forward.

### 4. ESBK Requirements

#### 4.1.

The ESBK game ID is one of the fields required for reporting on game sessions to the FGB. This ID will be provided by the regulator.

#### 4.2.

Approval is required before making any changes to the max bet limit. This means that if a game has made such changes for any other market, Switzerland cannot be included in baselining such change until operator’s have received approval for such change.

#### 4.3.

Changes the max bet limit range will require prior approval and may result in certification required.

#### 4.4.

Changes to critical files will require approval.

## Summary

The summarized list below shows the requirements that will require effort/config/development by Derivco:

- The Swiss franc and Euro will be the only supported currency.
- The casino languages that must be supported are: German, English, French, Italian.
- RTP must be displayed in help files
- RTP > 80%
- Playcheck is required.
- Games must be certified.
- Changes to critical files and/or max bet limits will require approval.