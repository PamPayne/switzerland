---
country: Switzerland
document_name: Switzerland Operator Guidelines
source_file: 009-961 MGS Casino - Operator Guidelines for Switzerland v3.0.pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# Switzerland Operator Guidelines

**Derivco - Internal**  
**Release Date:** 02 April 2020  
**Document No:** 009-961  
**Version:** 3.0  
**Regulated Market Casino Compliance**

## Contents

- Introduction
- Microgaming Solution
- Registration
- Currencies
- Languages
- Games
- Incomplete Games
- Player Protection
- Responsible Gaming
- Data Recording System
- Reporting

## Introduction

This document provides an overview for Microgaming Casino operators to comply with the regulations defined by the Swiss regulatory body.

Defines the split in responsibilities around managing players and games in the Swiss market, identifies what Microgaming will provide you with to satisfy the Swiss market requirements and assists you in ensuring that the correct integrations are done to satisfy the market requirements

## Microgaming Solution

The following table summarises the areas and where the responsibilities lie. These responsibilities are defined since Microgaming is not your primary platform and does not contain all the information necessary to manage certain aspects of your players’ life cycle.

| Component | Sub Component | Operator | Microgaming |
|---|---|---|---|
| General | Player Verification Services | Yes | No |
| General | Integration – Platform | Yes | No |
| General | Client Legislative Changes | Yes | Yes |
| General | Domain Re-direction | Yes | No |
| General | Platform Certification | Yes | Yes |
| General | License Application and Submission | Yes | Yes |
| Login | Login | Yes | No |
| Login | Online Registration | Yes | No |
| Login | Player Account Management | Yes | No |
| Login | Account Status | Yes | No |
| Login | Last Login Reminder | Yes | No |
| Login | Incomplete Games Dialog | Yes | No |
| Login | Languages & Currency | Yes | Yes |
| Login | Terms & Conditions and Gaming Contract | Yes | No |
| Lobby | Player Balance | Yes | No |
| Lobby | Player Protection Content | Yes | No |
| Lobby | Responsible Gaming (including deposit, limits, exclusions and time-outs) | Yes | No |
| Gaming | Game Certification | Yes | Yes |
| Gaming | RNG Certification | Yes | Yes |
| Gaming | Game Rules | Yes | Yes |
| Gaming | Display Game Rules | Yes | Yes |
| Gaming | Display Game Help | Yes | Yes |
| Gaming | Display RTP | Yes | Yes |
| Back Office | Account Migration | Yes | No |
| Back Office | Game Management | Yes | Yes |
| Back Office | Account Management | Yes | No |
| Back Office | Value Adds | Yes | No |
| Back Office | Banking | Yes | No |
| Back Office | Deposit | Yes | No |
| Back Office | Withdrawal | Yes | No |

## Registration

As Microgaming does not have any visibility into your registration process, you would need to manage this aspect as well as the document verification and account activation requirements for your players.

Please ensure that a player is not able to have more than one account registered per brand and only residents of Switzerland can register on your casino.

### Provisional Accounts

- Please ensure that you verify accounts provisionally opened no later than one month after the provisional opening.
- You need to ensure that as long as a player account has not been definitively opened the player may not transfer more than 1000 francs. The player may not draw their winnings.

## Currencies

The Swiss franc and Euro will be the only supported currency for wagers for participation in the games.

This is determined by the Player currency, so please ensure that your players register in Swiss franc or the Euro.

## Languages

The casino languages supported will be German, English, French, Italian.

All Game Rules and help files will be translated into the above-mentioned languages by Microgaming.

We will offer a mixture of fully-translated games, semi-translated games and English only games.

## Games

The following game changes will be implemented by Microgaming and included in Swiss casinos:

- Help Files
  - We shall display the RTP in all help files.
  - Microgaming will inform you of any significant changes via General Notifications as per any updates.
- Autoplay
  - AutoPlay will be available for players but limited to 100 spins.
  - The player will able to stop AutoPlay at any given moment, if enabled.
  - Stopping Autoplay:  
    Microgaming exposes two methods that are available in internet browsers. These are:
    - StopGamePlay
    - ReStartGamePlay

You must call the following on the iFrame:

document.getElementById(‘IFrame’) .contentWindow.postMessage  
(“StopGamePlay” , “https://quickfireessl.gamesassists.eu”);

- The first parameter on the postMessage call is the message we define.
- The second parameter on the postMessage call is the domain, including the http(s) of the hosted casino.
- Exception: The messaging protocol does not work for Internet Explorer (IE) 6 and 7.

## Incomplete Games

As Microgaming is not your primary platform and player accounts are owned by yourselves and multiple vendor’s games are offered, we would require you to retrieve any incomplete Microgaming game information for players using the Get Incomplete Games API method. You would need to complete any development required for the user interface, translations and game redirection.

A valid operator token must be provided in the Authorization header, this can be requested via your Account Manager.

The following request call with mandatory fields needs to be made:

### Request Call

GET /balances/product/productId/user/userId/incompleteGames

### Required Fields

| Name | Type | Format | Description |
|---|---|---|---|
| productId | Integer | int32 | The ProductId (previously called CasinoId or ServerId). This identifies the system where the account is held and can be either a SessionProductId or RegisteredProductId. |
| userId | Integer | int32 | The UserId of the account. |

After a request call is initiated a response will be sent back that will either be a successful or an unsuccessful (error) attempt. If successful, the below information is displayed:

### Responses

| Name | Type | Format |
|---|---|---|
| clientId The ClientId for the game. | Integer | int32 |
| moduleId The ModuleId for the game. | Integer | int32 |
| gameName The name of the game, e.g. HTML5 - Feature Slot - Avalon. | String | int32 |
| moduleName The name of the module, e.g. Feature Slot - Avalon. | String | int32 |
| payouts The combined amount owed to the user, e.g. a payout from a win in a game. | Number | Decimal |
| sessionId SessionId allocated for the session. | Integer | int32 |
| userTransNumber The UserTransNumber is the associated user transaction number for the incomplete game. | Integer | int32 |
| wagers The combined amount taken from the user, e.g. a bet taken during a game. | Number | Decimal |

The /accounts/CheckUserExists API method returns the UserId of the player. You can use this method to retrieve the UserId to do the Imcomplete games call.

### Responses

| Name | Type | Format |
|---|---|---|
| doesExist Indicates whether the specified Username exists or not | Boolean | int32 |
| registeredProductId The ProductId against which the account was created. What we called CasinoId or ServerId in the past. Only returned if the specified Username already exists. | Integer | int32 |
| suggestedUsernames Array of suggested alternate Username that are currently available. They are based on the provided username. Only returned if the specified Username already exists. | String |  |
| userId The UserID for the account, if the Username already exists | Integer | int32 |

## Player Protection

Player protection information must be accessible to players on the casino website. The content on Player Protection assists players in gaming responsibly. Since you manage the lobby for your casino, you need to provide the players with the following information in an easily accessible and easily understandable form:

- Information about the risks of the game;
- Information on opportunities for self-control, game restrictions and suspensions;
- Information about offers to support and treat addicted, indebted or addiction-prone persons and their surroundings, including addresses of counselling centers and self-help groups.

## Responsible Gaming

Responsible gaming measures need to be in place to ensure that all players play responsibly and are in control of managing their gaming activity. Since Microgaming operators own the player accounts and manage their own lobby, you must ensure that the following responsible gaming options are accessible to your players:

- Wager and Loss Limits
  - The player must have an option to set their wager or loss limits over 3-time periods: daily, weekly and monthly.
  - The player must be able to adjust the maximum amount they have set at any time.
  - Lowering a maximum amount will be effective immediately. Increases will be effective after 24 hours at the earliest.
- Self Exclusions
  - An internal exclusion system must exist that allows the player to self-exclude.
  - Players who self-exclude cannot participate in games or deposit.
  - Data recorded in the exclusions register must be retained for four years after which it must be deleted.
  - Voluntary player exclusions may only be lifted after three months.
- Suspensions
  - You can suspend players from gaming, of whom you know or must assume:
    a) are over-indebted  
    b) place stakes that are disproportionate to their income and assets.  
    c) are addicted to gambling.
  - The suspension must be communicated to the person concerned in writing with justification.
- Temporary Games Withdrawal
  - Players must be allowed to exclude themselves from the game for a certain time, selected by the player, for a maximum however of six months.
  - Players must be allowed to exclude themselves from one, several or all game categories.
  - Players may not themselves amend the duration of the temporary game withdrawal before the period is over.
- Self Tests
  - Players need to be provided with a self-assessment questionnaire to check their own gaming behaviour.
- Error Codes
  - To enable the Microgaming system to display informative error messages to players, we require that the following error codes are returned under the prescribed conditions.

| Code | Description |
|---|---|
| 6102 | Account is locked. |
| 6104 | Player is self-excluded. |
| 6109 | Self-exclusion is over and the player must contact the operator to lift the exclusion. The cooling period is effective once this is done. |
| 6110 | Self-exclusion is over but the player is in the cooling period. |
| 6112 | Player is deactivated. |
| 6113 | Player is self-excluded on registry |
| 6503 | Player has insufficient funds. |
| 6505 | The player exceeded their daily protection limit. |
| 6506 | The player exceeded their weekly protection limit. |
| 6507 | The player exceeded their monthly protection limit. |
| 6508 | The player exceeded their game play duration. |
| 6509 | The player exceeded their loss limit. |
| 6510 | The player is not permitted to play this game. |
| 6114 | The player has exceeded his daily login duration limit |
| 6115 | The player has exceeded his weekly login duration limit |
| 6116 | The player has exceeded his monthly login duration limit |

## Data Recording System

As Microgaming is not your primary platform and multiple vendor’s games are offered please ensure that you configure a Data Recording System environment that registers data the regulator requires, in order to:

a. verify the determination of the gross gaming revenue and all financial transactions;  
b. control game security and transparency;  
c. monitor the implementation of the social concept;  
d. monitor compliance with the due diligence obligations to combat money laundering and financing terrorism.

Please ensure that online access is available for the regulator for at least five years after the transfer of the casino tax. The Data Recording System servers are required to be in Switzerland

## Reporting

Since Microgaming is not your primary platform and player accounts are owned by yourselves, you are required to produce reports defined in the legislation for reporting purposes.

We shall provide you with data, where applicable, for all Microgaming games in order for you to fulfil your reporting requirements.

We believe that the items identified in Article 39 in the Casino Regulations document, are only required to be recorded and stored in our systems. Information may be requested via the Assist application on a case-by-case basis.

Please refer to the table below. For each item of information needed for reporting, we have provided feedback on how this can be obtained or if the responsibility lies solely with you.

| Legislation | Field | Operator | GGI |
|---|---|---|---|
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | date and time of the start and end of the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | player identification; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | game session identification; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | identification of the game and table; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | game played, game version and whether it is run in one or several casinos; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | number of game units in the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | total amount of all bets in the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | total amount of all winnings in the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | total amount of free game credits used in the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | total amount of free game credits won in the game session; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | list of winnings subject to withholding tax; | X | X |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | data on the player account at the end of the game session in particular the redeemable and non-redeemable amounts; | X |  |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | total amount of collected commissions for games jointly run by several casinos; | X |  |
| Point 1 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS): At the end of every game session the following data must be collected by the data recording system (DRS): | date and time of the data collection | X | X |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of all payments by players to their player account; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of all purchases by players from their player account; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of the players’ redeemable credit balance; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of the players’ non-redeemable credit balance; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of all bets; | X | X |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of all winnings; | X | X |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | number of player accounts; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of commissions for games jointly run by several casinos; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of free game credits converted to redeemable credits; | X | X |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of bets for games jointly run by several casinos; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of winnings for games jointly run by several casinos; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | total amount of withholding tax deductions; | X |  |
| Point 3 - Art. 39 Data collected by the DRS on online games (Art. 60 VGS) At the end of every day the DRS must create a summary of all operations on the day concerned and which must in contain the following information | date of the recorded day and date and time of the data collection | X | X |