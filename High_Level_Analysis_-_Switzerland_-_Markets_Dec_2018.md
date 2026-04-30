---
country: Switzerland
document_name: High Level Analysis for Switzerland Regulated Market
source_file: High Level Analysis - Switzerland - Markets Dec 2018.pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# High Level Analysis for Switzerland Regulated Market

## Contents

- [SUMMARY](#summary)
- [POTENTIAL AREAS OF CONCERN](#potential-areas-of-concern)
- [LEGISLATION](#legislation)
- [OPERATIONAL REQUIREMENTS](#operational-requirements)
- [REGISTRATION](#registration)
- [FEATURE REQUIREMENTS](#feature-requirements)
- [FIELD REQUIREMENTS - IDENTITY](#field-requirements---identity)
- [STATUSES](#statuses)
- [LANGUAGE AND HELP](#language-and-help)
- [EXTERNAL REGISTER CHECKS](#external-register-checks)
- [LOGIN](#login)
- [BANKING](#banking)
- [RESPONSIBLE GAMING & SELF RESTRICTION REQUIREMENTS](#responsible-gaming--self-restriction-requirements)
- [GAMES](#games)
- [BACKOFFICE UPDATES](#backoffice-updates)
- [DAILY ACCOUNT AND GAMING LOGS AND SECURITY](#daily-account-and-gaming-logs-and-security)
- [AUDITS/CERTIFICATION/TESTING](#auditscertificationtesting)
- [DATA RECORDING SYSTEM AND BACKUP](#data-recording-system-and-backup)

## Summary

## Potential Areas of Concern

This document includes a high-level analysis for Switzerland. We still need clarification on several regulations. What stands out, is:

- An online partner is required;
- We might need integration to external registers;
- We must provide a Data Recording System, however, not clear if the source code needs to be in Switzerland.

This only includes Casino; Sportsbook and Poker excluded.

## Legislation

| Description | Value |
|---|---|
| dated 29th September 2017 The Federal Assembly of the Swiss Confederation, based on Article 106 of the Federal Constitution1, after considering the Federal Council's message of 21st October 2015 2, | Federal Law on Gambling (Money Gaming Act, BGS) |
| English Federal Law on Gambling. Referred to as BGS | 7 November 2018 |
| Art. 52 Repeal of the previous law The Ordinance of the FDJP of 24 September 20044 on Surveillance Systems and Gambling is repealed. Art. 53 Entry into force 1 This Ordinance will enter into force, subject to Section 2, on 1 January 2019. 2 If the validation of the results of the referendum of 10 June 2018 occurs only after 24 December 2018, this Ordinance will enter into force on 1 January 2020. | Ordinance of the FDJP on Casinos (Casino Ordinance FDJP, [Spielbankenverordnung] SPBV-FDJP) Casino regulations – 23.11.2018 Referred to as Casino Regulations |
| (Gambling Ordinance [Geldspielverordnung], VGS) of 7. November 2018 | Ordinance on Gambling GamingRegulations_EN - 23.11.2018 Referred to as Gaming Regulations |
| Ordinance of the FDJP on the Due Diligence Obligations of Organisers of Large Scale Events to Combat Money Laundering and Financing Terrorism (Money laundering ordinance FDJP, [Geldwäschereiverordnung] GwV-FDJP) The Federal Department of Justice and Police (FDJP), based on Article 17 of the Anti-Money Laundering Act of 10 October 1997 1 (AMLA) and Articles 67 (4) and 68 (4) of the Gambling Act of 29 September 2017 2 (BGS), | AML Ordinance Referred to as AML. |

## Operational Requirements

The list below describes the high level operational requirements which would need to be fulfilled according to regulations for Switzerland. The list is a guideline and shall not be understood as an exhaustive list which guarantees compliance.

## Registration

## Feature Requirements

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Age Limit | English Federal Law on Gaming (BGS) Art 72: "Protection of minors 1 Minors must be especially protected. They are not to be allowed to participate in casino games and in the board-games conducted online." 2 For the other board games, the inter-cantonal authority decides, depending on the risk potential, the age that entitles the holder to participate. It must not be less than 16 years. Gaming Regulations Art. 47.3 d ‘Opening of a player account’ ‘a is a legal adult. | Adult is 18, appears that legal age is 18, to confirm. We are compliant. Other board games not applicable to us. |
| 2 | Single Player account | Gaming Regulations Art 47.2 The organiser will open only one account per player. | Compliant – we can restrict per licencee. |
| 3 | Requirements for an account: | Gaming Regulations Art 48 3a-d: 3 They will only open the player account when the player: a. is a legal adult; b. is domiciled or ordinarily resident in Switzerland; c. is not affected by any player suspensions (Art. 80 BGS) and d. is not subject to any player bans (Art. 52 BGS), where this concerns an organiser of a casino. | 18 years old – compliant. Domiciled in Switzerland or ordinary resident – need to confirm if can play if outside Switzerland. Not affected by player suspension – we are compliant, would have to integrate once we have the technical requirements – not sure of amount of dev. |
| 4 | Restriction List | Gaming Regulations Art 48 3 (above) c and d – not suspended. BGS Art 52 states who will be suspended | Integration to check suspension. |
| 5 | External Register | BGS Art 80 Suspension 1 The casinos and organisers of online board games suspend persons from the gaming operation, of whom they know or must assume, on the basis of their own perceptions or on the basis of reports from third parties, that they: a. are over-indebted or do not meet their financial obligations; or b. Place stakes that are disproportionate to their income and assets. 2 They also suspend people from the gaming operation of whom they know or must assume, that they are gambling addicts, from a report by a specialist or social security authority. 3 The inter-cantonal authority may extend the game suspension to other board games as part of the game permits. It can ensure the exclusion of these additional games by setting a threshold limit and having the payout of the underlying winnings blocked. 4 Suspension of the game covers casino games, board games played online and board games to which the inter-cantonal authority has extended the suspension under paragraph 3. 5 The gamblers can apply for a suspension to a casino itself or to an organiser of board games, who impose the suspensions. 6 The suspension must be communicated to the person concerned in writing with justification. | BGS Art 80 refers that Casino can suspend and gambler can apply for suspension. Development would probably be required to integrate with a system to do these checks, no details of this available at this time. It also does not specify when checks need to be done, assume registration and login. |
| 6 | Terms and Conditions | Operators need to manage their own terms and conditions. | No specific requirements. |

## Field Requirements - Identity

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Minimum requirements | Gaming Regulations Art. 48 Minimum information for opening an account a. Surname, forename b. Date of Birth; c. Residence or temporary address | Compliant |
| 2 | Verification of Identity | Gaming Regulations Art. 49 Verification of Identity 1 The organiser will open the player account when they have verified that the player information conforms with the facts and where the requirements of Article 47 (2) and (3) have been fulfilled. | Single Account, adult, domiciled in Switzerland, no suspensions. Basic requirements – compliant. |
| 3 | Proof of Identity | 2 Proof of identity may be by way of: a. a copy of an official ID; b. an electronic identity; or c. any other equivalent means permitted by the competent supervisory authority. | We have the ability in Caiman to record ID verification. If we need to integrate, there will be development. Operator responsibility to keep the records. |

## Statuses

A full range of player statuses with associated actions will need to be provided. We are compliant with this, but it needs to be customized for Switzerland.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Provisional | Gaming Regulations Art. 52 Provisionally opening a player account 1 The organiser can provisionally open a player account, where they: a. have received the information listed in Article 48; b. have determined, on the basis of the player’s details, that the requirements of Article 47 (3) have been fulfilled; c. have established that the player is not listed on the register of blocked players; and d. there is no specific reason to believe that the player's details do not conform to the facts. 3 As long as the player account has not been definitively opened the player may not transfer more than 1000 francs and the player may not draw their winnings. 4 If the organiser establishes that the player does not fulfil the requirements of Article 47 (3), any credit balance will be transferred to a payment account under their name; at most the total of the amounts the player has paid will be transferred. Any excess will be transferred to the AHV state equalisation fund, where this concerns a casino, or for non-profit purposes, where this concerns an organiser of large scale events. | Account can only be in Provisional pending checks for one month. Player can log in and wager. Max deposit of 1000 francs No withdrawal. |
| 2 | Activated | Gaming Regulations Art. 52 2 The organiser will verify the identity in accordance with Article 49 no later than one month after the provisional opening. If the player fulfils the requirements set out in Article 47 (3) the player account will be definitively opened. Gaming regulations Art. 47 Opening a player account 1 Anyone who wants to access an online gambling service requires a player account with the organiser. 2 The organiser will open only one account per player. 3 They will only open the player account when the player: a. is a legal adult; b. is domiciled or ordinarily resident in Switzerland; c. is not affected by any player suspensions (Art. 80 BGS) and d. is not subject to any player bans (Art. 52 BGS), where this concerns an organiser of a casino. Gaming Regulations Art. 49 Verification of identity 2 Proof of identity may be by way of: a. a copy of an official ID; b. an electronic identity; or c. any other equivalent means permitted by the competent supervisory authority. | Complaint -standard status management. Activate after verification within one month. 1. Operator to activate accounts based on docs received. 2. Only once players details are verified, can the account be activated. 3. Able to log in and wager 4. Able to withdraw funds Compliant – need verification of what ‘other equivalent’ roof of ID is. |
| 3 | Deactivated | Gaming Regulations Art 52. 4 If the organiser establishes that the player does not fulfil the requirements of Article 47 (3), any credit balance will be transferred to a payment account under their name; at most the total of the amounts the player has paid will be transferred. Any excess will be transferred to the AHV state equalisation fund, where this concerns a casino, or for non-profit purposes, where this concerns an organiser of large scale events. | Not sure what status this will be, but we are compliant with status management. If account cannot be activated after 1 month, player can receive his payment, balance to AHV state fund – operator responsibility – similar to Italy. |
| 4 | Suspended | BGS Art 80 Suspension 1 The casinos and organisers of online board games suspend persons from the gaming operation, of whom they know or must assume, on the basis of their own perceptions or on the basis of reports from third parties, that they: a. are over-indebted or do not meet their financial obligations; or b. Place stakes that are disproportionate to their income and assets. 2 They also suspend people from the gaming operation of whom they know or must assume, that they are gambling addicts, from a report by a specialist or social security authority. 3 The inter-cantonal authority may extend the game suspension to other board games as part of the game permits. It can ensure the exclusion of these additional games by setting a threshold limit and having the payout of the underlying winnings blocked. 4 Suspension of the game covers casino games, board games played online and board games to which the inter-cantonal authority has extended the suspension under paragraph 3. 5 The gamblers can apply for a suspension to a casino itself or to an organiser of board games, who impose the suspensions. 6 The suspension must be communicated to the person concerned in writing with justification. | Winnings are blocked. Check if withdrawal allowed? Casino can suspend player or player can apply. Might require integration to a register. |
| 5 | Self-Excluded | BGS Art 80 5 The gamblers can apply for a suspension to a casino itself or to an organiser of board games, who impose the suspensions. Gaming Regulations Art. 89 Temporary game withdrawal 1 The organiser of online games will provide the player with a means of temporarily withdrawing from the game for a certain time, selected by the player, for a maximum, however, of six months. | Player opts and requests suspension (permanent or for a period) Access allowed to be clarified. Standard status management. Must be able to integrate and support the exclusions as set out by the external register. Integration to register to be clarified. Temporary self-exclusion – 6 months max |
| 6 | Re-activated | BGS Art 81 - Cancellation of the suspension 1 The suspension must be lifted at the request of the person concerned, if the reason for it no longer exists. 2 The application must be submitted to the casino or the organiser of board games, which has issued the ban. 3 The cancellation procedure must include a canton-recognised specialist or department. | Reactivation by the Operator. Application by player. Reactivation subject to verification (authorization by specialist – how?) Need to know process, integration might be required. |
| 7 | Closed | Gaming Regulations Art. 51 Closing a player account 1 The organiser will close the player account when: a. the player requests this; b. they determine that the player no longer fulfils the requirements laid out in Article 47 (3); or c. the player account has been inactive for more than two years. 2 Any credit balance will be transferred to a payment account in the name of the owner of the player account. 3 If the account details of the player are not valid and the organiser cannot contact the player, despite efforts, which are reasonable and proportionate, with regard to the amount concerned, the player's credit will be kept at their disposal for two years. After this period of time the credits will be transferred to the AHV state equalisation fund, where this concerns a casino, or for non-profit purposes, where this concerns an organiser of large scale events. 4 The organiser will transparently inform the players about the consequences of invalid account details and long player account inactivity. | Close account on request, not fulfilling requirements, inactive for more than 2 years. Transfer credit balance to player, if details not correct, keep for 2 years and then transfer to AHV state fund. Operator must inform player of consequences of account inactivity. Could include in terms and conditions. |

## Language and Help

Language is not specified, just that it needs to be clear. Casino content provided by Microgaming and translated into German, French and Italian includes:

- Games
- Help files
- PlayCheck
- Cashcheck
- Responsible Gaming
- Clients
- Microgaming Lobbies
- Microgaming Banking solution

It is the operator’s responsibility to translate bespoke, self-developed content.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Help files | Gaming Regulations Art. 43 Gaming rules (Art. 44 BGS) 1 The casino or organiser of large scale events will provide the players with the rules of play or a summary of the rules of play for each game type. 2 The rules of play or the summary of the rules of play must be in easily understandable language and the players must have easy and direct access to these. 3 The FDJP will determine the minimum information of the rules of play for casino games. 4 The casino will issue the rules of play for the table games offered by the casino and will submit these to the FGB prior to authorisation. | Rules must be in an easily understandable language – our translations include German, French and Italian. We will have to comply with the minimum required information. Players must have easy access – we comply, will have to re-evaluate if further once we have specifics, but our help is easily accessible. |
| 2 | Translation | Gaming Regulations Art. 43 2 The rules of play or the summary of the rules of play must be in easily understandable language and the players must have easy and direct access to these. | The official languages in Switzerland is German, French and Italian. There is also another language, Romansh, but based on the requirement, our current translations should be sufficient, and this includes include English, German, French and Italian. |

## External Register Checks

It appears that Integration with an external register is required to facilitate checks at time of registration and login to check status – not sure if there is a way to check identity.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | External Register | Gaming Regulations Art. 85 Data in the register of blocked persons (Art. 82 BGS) 1 The casino or organiser of large scale events will record the following information on blocked persons as per Article 80 BGS in the register: a. surname and forename; b. date of birth; c. nationality; d. nature of the imposed suspension e. issue date of the suspension f. reason for the suspension 2 As soon as a player suspension is lifted the data of the person concerned may no longer be accessed by other casinos or organisers of large scale events. 3 The casino or organiser of large scale events will ensure the register is kept correctly. 4 Blocked persons may contest their entry in the register with the casino or organiser of large scale events. | Need details on how the register will work. |

## Login

Verification of player status on login. In addition, might have to a check against the external register at time of time of login.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Verification | There are no details with regards to login checks and how this is done, however, the status change requires it. | Please refer to statuses. We will need to check statuses of provisional players to activate if document provided or de-activate after 30 days id not as well as exclusions. We are compliant with status management, more detail required. |

## Banking

A compliant banking solution will need to be developed, which includes limitations on deposits and withdrawals for Provisional Players.

The only currency discussed is the Swiss Franc, however, no restrictions are mentioned. We can offer one or multiple currencies. Swiss Franc can be displayed as CHF, Fr., Fr.sv. – CHF is the ISO code. So, one thousand Swiss Francs displays as CHF 1,000.00.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Currency | No currency specified, but the legislation only mentions Francs. | We are compliant with single or multi-currency. No mention of what to display either. |
| 2 | Minimum deposit for Provisional players)1,000 francs) | Gaming Regulations Art. 52 Provisionally opening a player account 3 As long as the player account has not been definitively opened the player may not transfer more than 1000 francs and the player may not draw their winnings. | Limit provisional accounts to 1000 francs deposit and may only withdraw 1000, not winnings. |
| 3 | Free Games and Free Credits | 4 The casinos will keep separate accounts for free games and free game credits. | Mentions that the Casino will keep separate balances and it is also not part of gross gaming revenue – Gaming Regulations Art 133 (1 Bets, which are free for players due to the free games or free game credits authorised by the FGB, do not constitute part of the gross gaming revenue). So, we need to clarify if it needs to be displayed separately for the player but does not appear this is required. |

## Responsible Gaming & Self Restriction Requirements

The requirements are standard, except for the fact that player need to be able to set a bet and/or loss limit daily, weekly and monthly. We do not offer this and need to determine if our current offering for responsible gaming will suffice.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Restrict game play | Gaming Regulations Art. 89 Temporary game withdrawal 1 The organiser of online games will provide the player with a means of temporarily withdrawing from the game for a certain time, selected by the player, for a maximum, however, of six months. 2 The player can choose whether they want to temporarily withdraw from one or several categories of games or from all games offered by the organiser. 3 They may not themselves amend the duration of the temporary game withdrawal before the period is over. Upon a justified application the organiser may revoke the temporary withdrawal where they have determined that the requirements for blocking as per Article 80 BGS have not been fulfilled. | We do not offer the ability to withdraw from categories of games, so it will have to be exclusion, or it will require a lot of development. |
| 2 | Advertising | BGS Art. 74 Advertising 1 Gambling organisers may not advertise in more obtrusive or misleading ways. 2 Advertising must not be directed at minors or persons who have been barred. 3 Advertising for Gambling not authorised in Switzerland is prohibited. | Operator responsibility |
| 3 | Gambling Warning | Casino Regulations Art. 48 Social concept (Art. 77 Gambling Act) 4. Chapter: Protecting players from excessive gambling The casino will, with regard to the features of their distribution channel, outline in their social concept, in particular; a. mode, form and content of the information they provide to the players as per Article 77 of the Gambling Act of 29 September 20172 (BGS); b. observation criteria, methods, means and instruments used to ensure early recognition of players at risk of gambling addiction and the measures provided; c. measures they offer to players for self-regulation, game restrictions and game moderation and the interventions and measures provided; d. processes to verify the requirements of player suspensions including the means and instruments used; e. processes to initiate and repeal player suspensions including the means and instruments used; f. rolls and competencies of involved, external experts, in particular in the process for repealing player suspensions; g. training programme with information on the training type, the functions of the participants, the duration, the content and the trainers used; h. organising and maintaining documentation as per Article 49. | This is the operator responsibility |
| 4 | Game Restrictions and self-regulation | Gaming Regulations Art 87 1 From the opening of the player account the player must, at all times, have easy access to the following information on their gaming activity during a specific time period: a. bets; b. winnings; c. net result of the gaming activity. | Playcheck and cashcheck provides this information. |
| - | Loss and bet limits | 2 From the opening of the player account the organiser will demand that the player set one or more maximum amounts they wish to limit their daily, weekly or monthly bets or losses to. | We cannot limit bets or losses, and it needs to be set on registration. Will deposit limits and session time-outs suffice? |
| - | Max bet settings | 3 For large scale events, where there is a low risk potential for the player, the organiser may forgo the demand to set a maximum amount. They must, however, give the player the opportunity to set a maximum amount at any time. | We are compliant with min and max bet. |
| - | Increases and decreases | 4 The player must be able to adjust the maximum amount they have set at any time. Lowering a maximum amount will be effective immediately. Increases will be effective after 24 hours at the earliest. | We are compliant for deposit limits. |
| 5 | Play timer | Art. 39 Data collected by the DRS on online games (Art. 60 VGS) 1 At the end of every game session the following data must be collected by the data recording system (DRS): a. date and time of the start and end of the game session; b. player identification; c. game session identification; d. identification of the game and table; e. game played, game version and whether it is run in one or several casinos; f. number of game units in the game session; g. total amount of all bets in the game session; h. total amount of all winnings in the game session; i. total amount of free game credits used in the game session; j. total amount of free game credits won in the game session; k. list of winnings subject to withholding tax; l. data on the player account at the end of the game session in particular the redeemable and non-redeemable amounts; m. total amount of winnings from connected jackpots and won during the game session; n. total amount of jackpot amounts in connected jackpots deducted in the game session o. total amount of collected commissions for games jointly run by several casinos; p. date and time of the data collection as per a-n. | Not specified, there is a requirement to record all session as per art 39 on left. |
| 6 | User Account History - Cashcheck | Casino Regulations Art 14. 1 The electronic counters must record the following data for every offered game: a. the entire amount of game credits used in all games played; b. the entire amount of game credits won in all games played; c. the entire amount of all games units conducted; d. the entire amount of registered game credits for every opportunity to acquire game credits; e. the entire amount of game credits paid out for every payout opportunity. | Cashcheck – compliant. This does seem to be landbased, but assume same requirement for online. To confirm. |

## Games

.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | RTP | Casino regulations Art. 5 Payout ratio All casino games must have a theoretic payout ratio of at least 80 per cent, but a maximum of 100 per cent. | . |
| 2 | Games of skill | BGS Art 3 - d. Games of skill: Gambling, in which the game proceeds depend entirely or predominantly on the skill of the player; e. Board games: Lotteries, sports betting and games of skill, each being automated, inter-cantonal or online; | No Poker/ Sportbook – does this refer to online Poker? We don’t have lotteries |
| 3 | RNG (Random number generator) & Game errors | Gaming Regulations (Art. 42 (3) BGS) 1 The safety concept of the casino or the organiser of large scale events should be set up to limit risks, prevent errors and to continuously optimise the processes. | No details. |
| 4 | Tournaments | BCS Art 16 3 SFGB can also allow the licensee to conduct small poker tournaments. BGS Art 35 - Additional preconditions for small poker tournaments 1 The following preconditions must be met for the permit for a small poker tournament to be granted: a. The number of participants is limited; they play against each other. b. The entry fee is low and commensurate with the duration of the tournament. c. The sum of the game proceeds equals the sum of the entry fees. d. The game is played in a publicly accessible location. e. The rules of the game and the information for the protection of participants from excessive gambling are published. | N/A – not going in with Poker |
| 5 | Game Rules/Help | Casino Regulations Art. 30 (Art. 43 VGS) 3. Chapter: Operation 1. Section: Rules of play 1 The rules of play will, at least, contain information on: a. course of play; b. manner of placing bets; c. minimum and maximum bets; d. winning opportunities; e. for table games: procedure, how the players are identified and their tasks and responsibilities. | Our help files are compliant with the rules. |

## Backoffice updates

Backoffice tools will need to be updated to support Switzerland requirements including but not limited to:

- Help Desk
- Financial Transactions (limits)
- Update Account Status
- Document verification
- Support of new Responsible Gaming requirements
- Reporting – statuses, limits and new Responsible Gaming requirements

## Daily Account and Gaming Logs and Security

There could be a SAFE type solution required; if so, it will need to be developed to support this.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | General storage | Gaming Regulations Art. 60 Data Recording System (Art. 42 BGS) 1 Casinos that run online gambling will operate a Data Recording System (DRS) in Switzerland. 2 They will register data the FGB needs in the DRS, in order to: a. verify the determination of the gross gaming revenue and all financial transactions; b. control game security and transparency; c. monitor the implementation of the social concept; d. monitor compliance with the due diligence obligations to combat money laundering and financing terrorism. | Not sure if this is a separate system or if integration is required. Need to determine if we need a server in Switzerland, but does not appear so – just a record. |
| 2 | Financial records/Data Storage | Casino Regulations Art. 41 Data storage (Art. 61 VGS) 1 The data in Articles 38 and 40 (1) must be taken, unamended, from the automated gambling games connected to the EACS and stored (raw data). They must be protected against any changes. 2 The FGB will provide the casinos with forms for the data transfer. 3 The amounts used to determine the gross gaming revenue, which are reported by the EACS on the basis of raw data and have been rectified due to malfunctions, in particular, must be correspondingly labelled and duly justified. | Specifies data that should be retained – not clear if this only applies to landbased, or to both. If for online, determine if reporting or integration to SAFE required. |
| 3 | Gaming Records | Casino Regulations Art. 46 Documentation of the casino games 3 In relation to the online casino games the FGB may demand the following information and documents: a. name and address of the supplier and manufacturer, where the manufacturer is not identical to the supplier; b. description of the hard and software used such as schemes and flow charts; c. information on the running of the game; d. description of the testing procedure used; e. function and structure of the random number generator; f. manner in which the individual game events and game results come about; g. maximum winnings per game unit; h. manner of assessing and results of the game statistics; i. number and results of the test games or play simulations; j. payout ratio; k. competition chances; l. source code; m. methods for clearly identifying the game; n. a certificate or a confirmation and the test report of an entity as per Article 62 VGS which shows that the online casino games comply with the statutory requirements. | May request documentation regarding source code. Need to clarify this requirement. |
| 4 | Security | Gaming Regulations Art. 65 IT security of online games 1 The IT security management of casinos, which run online games, must be certified as per the Norm ISO/IEC 27001 or ensure comparable security with other measures. 2 The casino may only acquire online games from suppliers who meet the requirements of Section 1. | We are ISO certified. |
| 5 | Reporting to regulator | Gaming regulations Art. 64 Reporting obligation 1 The casino will report to the FGB without delay: a. unusual incidents in one of the connected games; b. the breakdown or significant disruption of the EACS or the DRS. 2 The FGB will decide on the further action and further use of the data affected by the incident. Before this decision no data may be deleted or destroyed. | We will need to assist operators with reporting to the regulator. |
| 6 | Annual Casino Report | BCS Art 84 Report The casinos and organisers of board games submit an annual report to the competent enforcement authority on the effectiveness of the measures taken to protect gamblers against excessive gambling. | Operator responsibility |
| 7 | Annual Security Report | BCS Art 48 Reporting 1 The casinos and organisers of board games submit an annual report to the competent enforcement authority. 2 They make an annual report to the competent enforcement authority on the implementation of the security concept. | Annual Security Audit should satisfy this requirement. To confirm. |

## Audits/Certification/Testing

Audits and certification must be executed, as well as testing, but more guidelines are required.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Assessment | EF Art 97/ 98 - 1 Apart from fulfilling other tasks conferred on it by this law, SFGB has the following tasks: a. It monitors the compliance of legal 1. the management bodies and the gaming operation of casinos, 2. the compliance with the obligations for prevention of money laundering, 3. the implementation of the security and social policy. b. It assesses and levies casino tax. c. It fights against illegal gambling. d. It works with domestic and foreign supervisory bodies. e. It reports the Federal Council annually about its activity and publishes the report; the report also includes information about financial statements, balance sheets and reports of casinos. Authorisation To fulfil its tasks, the SFGB can especially: a. ask for the necessary information and documents from the casinos and the companies involved in manufacturing and trading of gambling facilities that supply the casinos; b. perform checks at casinos; c. ask for the necessary information and documents from auditing departments of the casinos; d. enlist the services of experts; e. give special tasks to the auditing department; f. f. Establish online connections for monitoring IT systems of casinos; | Audits and certifications required. Clarification regarding online connections for monitoring IT Systems of casinos; |
| 2 | Function Testing | Casino Regulations Art. 24 Function testing (Art. 21 VGS) 5. Section: Online casino games Before the launch of a new online casino game the casino must ensure, using appropriate tests, that the game functions correctly on their gaming platform. | No detail as to what testing is required. |

## Data Recording System and backup

No mention of DR, but a full data recording system must be available in Switzerland.

| No | Feature/Area | Requirements | Comments |
|---|---|---|---|
| 1 | Data Recording System | Gaming Regulations Art. 60 Data Recording System (Art. 42 BGS) 1 Casinos that run online gambling will operate a Data Recording System (DRS) in Switzerland. 2 They will register data the FGB needs in the DRS, in order to: a. verify the determination of the gross gaming revenue and all financial transactions; b. control game security and transparency; c. monitor the implementation of the social concept; d. monitor compliance with the due diligence obligations to combat money laundering and financing terrorism. 3 The FDJP will determine which data must be recorded in the DRS. 4 The DRS must be protected from unauthorised access. All subsequent changes to the stored data must be recognisable. 5 Before the launch and before any changes to the DRS the casino will provide the FGB with a certificate or a confirmation from an accredited conformity assessment body, which shows that the system complies with the statutory provisions. | A Data Recording System needs to be run in Switzerland and be accessible to the regulator. Some kind of integration might be required or might be just access. |
| 2 | Storing of Data/electronic accounting and control system | Gaming Regulations Art. 61 Storing the EACS and DRS data 1 The data necessary to determine the gross gaming revenue, in particular the invoices for the game tables and the EACS data, must be stored in a suitable form, at a secure location, for at least five years after the transfer of the casino tax. 2 The DRS data must be made available online, at the request of the FGB, for at least five after the transfer of the casino tax. | The data needs to be available online at the request of the regulator, for at least 5 years after tax transfer. It must be stored in a secure location. Not specified how it will be accessed. Take into consideration when archiving solution is developed. |
| 3 | Data to collect | Art. 39 Data collected by the DRS on online games (Art. 60 VGS) 1 At the end of every game session the following data must be collected by the data recording system (DRS): a. date and time of the start and end of the game session; b. player identification; c. game session identification; d. identification of the game and table; e. game played, game version and whether it is run in one or several casinos; f. number of game units in the game session; g. total amount of all bets in the game session; h. total amount of all winnings in the game session; i. total amount of free game credits used in the game session; j. total amount of free game credits won in the game session; k. list of winnings subject to withholding tax; l. data on the player account at the end of the game session in particular the redeemable and non-redeemable amounts; m. total amount of winnings from connected jackpots and won during the game session; n. total amount of jackpot amounts in connected jackpots deducted in the game session o. total amount of collected commissions for games jointly run by several casinos; p. date and time of the data collection as per a-p. | Data that needs to be collected and stored. Nothing we cannot provide. |