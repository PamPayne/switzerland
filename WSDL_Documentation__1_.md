---
country: Switzerland
document_name: WSDL_Documentation
source_file: WSDL_Documentation (1).pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# Technical specifications of Data Storage Device (DSD)

Date: 07.11.2018 / Version: esbk-onlinespiele-service-v1-wslib-1.0.6-20181011.113125-5-dist

With the introduction of the law on money games – foreseen to enter into force on January 1st 2019 - currently licensed Swiss casinos may obtain an extension to their concession in order to offer online casino games for the Swiss market.

According to art. 60 of the ordinance on money games, casinos with an extension of their concession to offer online casino games are required to operate a Data Storage Device (DSD) in Switzerland. The casino that is offering online casino games, must record all data in the DSD, allowing the Federal Gaming Board (FGB), as the surveillance authority, to supervise the determination of the gross gaming revenue (BSE/PBJ) and all financial transactions, to supervise the security and transparency of the game and to monitor the implementation of the plan of social measures and compliance with the obligations of anti-money laundering. The DSD must be protected from unauthorised access and every subsequent change of the data stored in the DSD must be traceable. The casino has to place the recorded data of the DSD at the disposal of the FGB.

The following criteria must therefore be fulfilled:

- Integrity: it must be possible to verify no data has been altered afterwards;
- Authenticity: it must be possible to verify the data was really written at the indicated time;
- Completeness: it must be possible to detect, if the data has been deleted afterwards.

The casino stores the data according to art. 39 and 40 of the ordinance on gambling houses into XML-messages, calculates checksums/hash values for the XML-messages and chains them up. Every end of day message will be complemented with a crypto-timestamp according to RFC3161 from a certified source. Each XML-message will be put in a datastore, wherefrom the XML-message can be retrieved at any time, checked for integrity, authenticity and completeness and sent to the FGB over a webservice-interface. These procedures (with the exception of storing and retrieving of the data from the datastore) are to be tested and certified by an accredited lab (cf. the blue rectangle of the attached drawing). The casino has to file a certificate to the FGB before putting the DSD into service initially and after each modification.

In addition, the casino and/or the provider of the DSD has the duty to fulfill its requirements concerning data protection, especially if third parties can access the data on the server (e.g. for maintenance).

Articles 39 and 40 of the ordinance on gambling houses define the data that has to be stored into the DSD. The format of the data to be stored in the DSD and to be transmitted to the FGB will be specified in the technical documentation of the FGB (including xsd-/wsdl-files). The data has to be sent over a webservice-interface to the FGB. The specifications of the XML-messages to be stored in the DSD are an integral part of the webservice-interface.

The technical specifications consist of a zip-file with the following folders (in alphabetical order):

- common-xsd: common definitions
- documentation: documentation-files
- esbk: .xsd- and .wsdl-files defining the XML-messages (casino-events-v1_0.xsd) and the webservice-interface (casino-events-import-service-v1_0.xsd and casino-events-import-service-v1_0.wsdl)
- samples: sample xml-files
- xslt: holding the file normalizeGameEvent.xslt used to normalise an XML-message prior to hash calculation

The casinos have to record data resulting from the online games as XML-messages in their DSD. These XML-messages are then to be sent over the webservice-interface. The casino transmits every message without delay to the FGB, whenever the webservice-interface is up and running. In case the webservice-interface should be down, casino operation can continue and the data is to be stored as before as XML-message in the DSD. When the webservice-interface is up and running again, transmission of the XML-messages to the FGB has to resume with the last XML-message that could not be sent.

The procedure to be followed is described as follows (with references to the attached drawing):

- Each XML-message has an unique identifier EventId e.g. in the form of a subsequent number or an UUID (cf. 1 in the attached drawing);
- In addition each XML-message holds the unique identifier and the hash of its predecessor (calculated upon creation of the predecessor) to form a chain of XML-messages (2);
- Each XML-message is hashed with the SHA-1 algorithm (4) and the calculated hash value is subsequently added to the XML-message (5) in hexadecimal representation (hex-string with 40 characters). In order to calculate the hash value, the field of the hash value has to be left empty and it will only be filled with the hash value after calculation of the hash value. The opposite has to be done for verifying the integrity of the message (i.e. clearing the hash field and then calculating the hash value over the message). Prior to calculation of the hash value, a normalisation (3) of the XML-message has to be performed with the file normalizeGameEvent.xslt (cf. explanations further down in this document);
- In addition, the end of day message, due to be generated every day after midnight, carries a field for a crypto-timestamp (6) according to RFC3161. This crypto-timestamp has to be built over the hash of the XML-message previously calculated and then inserted (7) into the XML-message. For all other types of messages this step has to be omitted;
- The XML-message is then stored in a datastore (8) so that it can be retrieved later for transmission to the FGB. The technology of the datastore is not prescribed by the technical specifications. This could be a database or a file system. The DSD has to have a built-in function allowing upon request to verify integrity, authenticity and completeness of the data of the whole datastore.

The casino transmits as follows each XML-message of the datastore over the webservice-interface (D) to the FGB:

- By first fetching (9) the next XML-message in line from the datastore;
- this XML-message has to be checked regarding integrity, authenticity and completeness (A) before sending. Should there be an error, the error has to be fixed before transmission of the XML-message;
- Whenever the webservice-interface is ready to receive messages, the casino sends directly the XML-message to the FGB. The FGB records the unique identifier of the last XML-message that has been correctly received by the FGB and is able to trigger an alert, in case the sequence is broken. The unique identifier of the last valid message is sent together with the alert to the casino. Thus the casino is able to resume and retrieve the next XML-message in line.
- The FGB can also request the resending of already transmitted messages, by replying with a different unique identifier that has been received last. The casino has then to resume transmission and continue from the XML-message that follows the XML-message with that unique identifier;
- The webservice-interface (D) allows transmission of up to 50 XML-messages (B) in the same SOAP-message at once to speed up transmission. Nevertheless, the order of the XML-messages needs to be respected. GZip-compression should be activated to reduce the amount of data to transmit.

The following XML-schema describes the form of the XML-messages to store and transmit over the webservice-interface. The schema also contains explaining text for every XML-element: casino-events-v1.xsd

## Comments

The webservice-client (C) of the casino uses a certificate enabling the casino to connect to the webservice-interface of the FGB. In order to receive this certificate, the casino has to fill out an application form and send it to the FGB.

Updates since the preview version: article numbers have been added, file “normalizeGameEvent.xslt” updated, new scenarios added, hashes of scenarios fixed, fractions of seconds removed in all sample data.

## Security of transaction

All XML-messages transmitted over the webservice-interface in the same SOAP-message were processed correctly, if there is no SOAP-Fault as answer by the webservice-interface. In the case of a SOAP-Fault, NONE of the transmitted XML-messages have been stored and all the XML-messages have to be resent.

## Interruption of the webservice-interface

There is no guarantee that the webservice-interface will be running 100% of the time. As soon as the webservice-interface is up and running again, transmission of XML-messages has to resume. The operation "GetLatestEvent" responds with the ID of the last XML-message that has been successfully received and processed by the FGB.

## PlayerId

Whatever the casino uses as PlayerId has to be unique, has to be constant over the whole duration the player is registered with the casino and has to be hashed with the algorithm SHA-1 before storing in the XML-message. Therefore the PlayerId of the XML-message does not contain any personal information but enables identification in the need of particular clarifications. Instead of calculating this hash each time whenever required, this hash can also be stored in the database of the casino together with the information of each player.

## EventHash

As already described before, each XML-message is to be hashed and the resulting hash value to be stored in the XML-element "EventHash". As XML-messages can hold the same data in slightly different ways (e.g. namespace definitions, namespace prefixes, newlines between elements, etc.), the XML-message has to be transformed to a normalised representation before hashing. The normalisation has to be done using the following XSLT-Stylesheet: normalizeGameEvent.xslt.

samples holds different sample messages with accurate hash value.

The following example with an end of day message explains this process:

### Example of an end of day message:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<e:DayEndEvent xmlns:e="http://ejpd.admin.ch/esbk/services/casino-events/v1">
<e:EventId>33f40aa4-f398-467d-85fd-0c49af8edb9a</e:EventId>
<e:PreviousEventId>201554a9-ba59-47cd-bd97-36fac44ea905</e:PreviousEventId>
<e:DateTime>2018-01-05T23:59:59</e:DateTime>
<e:EventHash>d1c71b0d3b88eab2d3172fc4713e1a3f1dd6163c</e:EventHash>
<e:PreviousEventHash>282d8234a5d74097f473955ee55149f067a4f57c</e:PreviousEventHash>
<e:CryptoTimestamp>MIIFRDADAgEAMIIFOwYJKoZIhvcNAQcCoIIFLDCCBSgCAQMxCzAJBgUrDgMCGg
UAMIIBtgYLKoZIhvcNAQkQAQSgggGlBIIBoTCCAZ0CAQEGBCoDBAEw
UTANBglghkgBZQMEAgMFAARA3je6S6khBQe3B1ZgW8G5vlK34BmgLa9ZsCa+tCRty0CNs1SMrjAT3yW
pwK0iR9Ut0sVqcTC1Jd/4OLqCRUo5xwIDCWXFGBYyMDE4MDkyMTA3NDIwOS4wN
zY1NzJaMAoCAQGAAgH0gQFkAQH/oIIBEaSCAQ0wggEJMREwDwYDVQQKEwhGcmVlIFRTQTEMMAo
GA1UECxMDVFNBMXYwdAYDVQQNE21UaGlzIGNlcnRpZmljYXRlIGRpZ2l0YWxseSBzaW
ducyBkb2N1bWVudHMgYW5kIHRpbWUgc3RhbXAgcmVxdWVzdHMgbWFkZSB1c2luZyB0aGUgZnJlZXRz
YS5vcmcgb25saW5lIHNlcnZpY2VzMRgwFgYDVQQDEw93d3cuZnJlZXRzYS5vcmc
xIjAgBgkqhkiG9w0BCQEWE2J1c2lsZXphc0BnbWFpbC5jb20xEjAQBgNVBAcTCVd1ZXJ6YnVyZzELMAkG
A1UEBhMCREUxDzANBgNVBAgTBkJheWVybjGCA1owggNWAgEBMIGjMIGVMREw
DwYDVQQKEwhGcmVlIFRTQTEQMA4GA1UECxMHUm9vdCBDQTEYMBYGA1UEAxMPd3d3LmZyZWV0
c2Eub3JnMSIwIAYJKoZIhvcNAQkBFhNidXNpbGV6YXNAZ21haWwuY29tMRIwEAYDVQQHE
wlXdWVyemJ1cmcxDzANBgNVBAgTBkJheWVybjELMAkGA1UEBhMCREUCCQDB6YYWDajpgjAJBgUrD
gMCGgUAoIGMMBoGCSqGSIb3DQEJAzENBgsqhkiG9w0BCRABBDAcBgkqhkiG9w0BCQ
UxDxcNMTgwOTIxMDc0MjA5WjAjBgkqhkiG9w0BCQQxFgQUGjda+YxSIWHI5TTajM4fjIjWBxswKwYLKoZI
hvcNAQkQAgwxHDAaMBgwFgQUkW2j2GDsyoLjS8WdF5Pn6WiHXxQwDQYJKoZ
IhvcNAQEBBQAEggIAFYiUy+UJwcpaJRdNjhYv387xo+rwXk4r8R2SWOQrpC5xgNOi7hNvXz9b+mJS9DTh
35jqPKbYQVGRk7EPUeygyvOl/Fj3m/l47zcy8qCoZiaHX4l7t1x4uWXBcSYU
F44JkDDot2SWy2z66vNGkUvRjwl3+wOxKuAgUYjhIuNtjYm6s446VkPADWYJybA5d6/qeSDPifaNMv7Gy+
H54f1GXrXESJMyzHACOeyoklYMcqGNcHdcD22/RdEJpr6RTwoYcouYhX5hl
yUtIat/mq/RIqVclMK/uPZzza5Pznt4/0fl7ZNCV3B6Ro8MAsgK6GI1NKY6BrTocYyUH5LdOGe9xejujWuZGQ
pcMxwHBpfcGvoDdcas+rIPUvKkgRI0qmz+g+xoIexvBuYnMS5FtgOa/K
0f1EFXCdQj00SLbv0XFA5I+JPV+lbhpCARESRh/coVfcYqvLs/d0Neks+O/3d9mjHCH1kIucQKxIfSmaRCaT/
XmUPTaD89DRHuu4shLDxZn7Ysb4m1RYI/CgQVeYEF9tDHfNQ/erEH7gi
lA6CTytBtnQAPMOiPh+Eb8mj9axOAagCwjlOY0Gr1D1ewWVbdiWMBgJWxWcm8LqVQg+2N0K6olgIciMkl
Hilq45qu78356tYbiU/5b6Gc2sLQaqvC6nm6P56gnixZD0L9gP5oXv8=
</e:CryptoTimestamp>
<e:TotalPayin>16200</e:TotalPayin>
<e:TotalPayout>5283.75</e:TotalPayout>
<e:TotalPlayerAccountsBalance>6618.75</e:TotalPlayerAccountsBalance>
<e:TotalPlayerAccountsBalanceNonRedeemable>123.55</e:TotalPlayerAccountsBalanceNonRedeemable

>
<e:TotalPlayerBets>177108</e:TotalPlayerBets>
<e:TotalPlayerWins>142756.50</e:TotalPlayerWins>
<e:TotalPlayerWinsFromExternalJackpot>0.00</e:TotalPlayerWinsFromExternalJackpot>
<e:TotalPlayerJackpotIncrementsForExternalJackpot>0.00</e:TotalPlayerJackpotIncrementsForExternalJa
ckpot>
<e:TotalPlayerRakeExternalGame>0.00</e:TotalPlayerRakeExternalGame>
<e:TotalBonusAmountRealised>0.00</e:TotalBonusAmountRealised>
<e:TotalPlayerBetsExternalGames>0.00</e:TotalPlayerBetsExternalGames>
<e:TotalPlayerWinsExternalGames>0.00</e:TotalPlayerWinsExternalGames>
<e:TotalDeductionTaxableWins>0.00</e:TotalDeductionTaxableWins>
<e:AmountOfPlayerAccounts>18</e:AmountOfPlayerAccounts>
<e:ReportingDay>2018-01-05</e:ReportingDay>
</e:DayEndEvent>
```

By applying the foresaid XSLT-Stylesheet, XML-declaration, namespace, newlines between elements, etc. are removed and the elements "EventHash" and "CryptoTimestamp" are ignored. The result is:

```xml
<DayEndEvent><EventId>33f40aa4-f398-467d-85fd-
0c49af8edb9a</EventId><PreviousEventId>201554a9-ba59-47cd-bd97-
36fac44ea905</PreviousEventId><DateTime>2018-01-
05T23:59:59</DateTime><PreviousEventHash>282d8234a5d74097f473955ee55149f067a4f57c</Previous
EventHash><TotalPayin>16200</TotalPayin><TotalPayout>5283.75</TotalPayout><TotalPlayerAccountsB
alance>6618.75</TotalPlayerAccountsBalance><TotalPlayerAccountsBalanceNonRedeemable>123.55</T
otalPlayerAccountsBalanceNonRedeemable><TotalPlayerBets>177108</TotalPlayerBets><TotalPlayerWin
s>142756.50</TotalPlayerWins><TotalPlayerWinsFromExternalJackpot>0.00</TotalPlayerWinsFromExtern
alJackpot><TotalPlayerJackpotIncrementsForExternalJackpot>0.00</TotalPlayerJackpotIncrementsForExt
ernalJackpot><TotalPlayerRakeExternalGame>0.00</TotalPlayerRakeExternalGame><TotalBonusAmount
Realised>0.00</TotalBonusAmountRealised><TotalPlayerBetsExternalGames>0.00</TotalPlayerBetsExter
nalGames><TotalPlayerWinsExternalGames>0.00</TotalPlayerWinsExternalGames><TotalDeductionTaxa
bleWins>0.00</TotalDeductionTaxableWins><AmountOfPlayerAccounts>18</AmountOfPlayerAccounts><
ReportingDay>2018-01-05</ReportingDay></DayEndEvent>
```

This chain of characters results in the hash value of "d1c71b0d3b88eab2d3172fc4713e1a3f1dd6163c".

## Cancellation Message

If there should be an error in a message, the message cannot just be removed, because this would break the chain. The message has to stay in the DSD and a cancellation message ("CancellationEvent") has to be put in the DSD. The cancellation message holds a reference on the message to be cancelled ("CancelledEventId").

E.g. the following XML-message with the EventId=476 should be cancelled:

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<PayoutTransactionEvent xmlns="http://ejpd.admin.ch/esbk/services/casino-events/v1">
<EventId>476</EventId>
<PreviousEventId>420</PreviousEventId>
<DateTime>2018-01-03T10:34:31</DateTime>
<EventHash>b179bdde5f11aab2b09c5927a10438c84bb5f729</EventHash>
<PlayerId>f2d47f9507c543fd0b8c42ae5ba44c737c1c8fe3</PlayerId>
<TransactionId>834</TransactionId>
<PlayerAccountBalance>134.25</PlayerAccountBalance>
<PayoutAmount>75.00</PayoutAmount>
</PayoutTransactionEvent>
```

The corresponding cancellation message, holding the EventId of the XML-message to be cancelled in the XML-element "CancelledEventId", would be:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<CancellationEvent xmlns="http://ejpd.admin.ch/esbk/services/casino-events/v1">
<EventId>513</EventId>
<PreviousEventId>512</PreviousEventId>
<DateTime>2018-01-04T10:23:12</DateTime>
<EventHash>34724153271ddd9de5492311bf34c2d0e7ffdf39</EventHash>
<CancelledEventId>476</CancelledEventId>
</CancellationEvent>
```

The cancellation message can be sent directly after the message to be cancelled. It can also be sent later on (max. 1 month later).

## Description of the XML-message types

This paragraph describes the different types of XML-messages that have to be created, stored in the DSD and sent over the webservice-interface.

### Transaction messages

The transaction messages are a family of 6 derived message types:

- **PayinTransactionEvent:** records the payment by a player that has been credited to the player's account. The XML-element "PayinAmount" holds the amount the player has paid to the casino to be put into his redeemable account;
- **PayoutTransactionEvent:** records a payout by the casino to a player. The XML-element "PayoutAmount" holds the amount the casino has paid to the player and is to be deducted from the player's account;
- **BonusInEvent:** records a transfer of bonus credits to the non-redeemable account of a player. The XML-element "BonusInAmount" holds the amount of bonus credits given to the player;
- **BonusRealisationEvent:** under certain conditions defined by the casino, a player may convert bonus credits into real money credits. These transfers are recorded using a "BonusRealisationEvent". The XML-element "BonusAmountRealised" holds the amount of bonus credits transferred from the non-redeemable account to the redeemable account of the player;
- **TaxableWinDeductionEvent:** single gains of more than 1 Mio. CHF are taxable wins and an anticipated tax of 35% has to be deducted by the casino and directly delivered to the tax authority. These transfers are recorded using a "TaxableWinDeductionEvent". The XML-element "TaxableWinDeduction" holds the amount of money deducted from the player's account;
- **PlayerStatusEvent:** status changes of a player account have to be registered in the DSD. These transfers are recorded using a "PlayerStatusEvent" message. The XML-element "PlayerStatus" holds the new status of the player. Valid status values are:
  - PROVISORY: after a new player's registration, the account normally gets the status of a provisory account. Except, if the verification of the player's details could be done at the same time;
  - VERIFIED: after verification of a player's details, the account of the player gets the status of a verified account;
  - CLOSED: whenever a verified player account is closed, its status turns to closed;
  - CLOSEDFROMPROVISORY: whenever a provisory player account is closed, its status turns to CLOSEDFROMPROVISORY.

### Game Session Message (GameSessionEvent)

The casino has to record one session message for every game session accomplished by a player. A game session comprises several spins as long as the same player is playing the same game or at the same table. Whenever the player changes the game or the table, the current session will be closed and stored. It is possible to have more than one session running for the same player at the same time (e.g. playing different slot games at the same time).

### End of Day message (DayEndEvent)

An end of day message is to be stored every day shortly after midnight. This message summarises key values of the last casino day. All transactions of the last day and all finished sessions of the last day have to be considered.

### Jackpot message (JackpotWinEvent)

One jackpot message has to be registered for each player winning a jackpot win that has not already been included in the session message in which session the jackpot has been won.

## Target Namespace

http://ejpd.admin.ch/esbk/services/casino-events-import/v1

## Port GameEventSynchronizationPort Port type

### Location:

http://localhost:8080/osba/ws/services/SynchronizGameEvents/v1

### Protocol:

SOAP

### Default style:

document

### Transport protocol:

SOAP over HTTP

## Operations:

1. GetLatestEventDetail
2. InsertEventsDetail

## Operations

### Port type GameEventSychnronizationServicePort

### 1. GetLatestEvent

**Description:**  
Request the last EventId transmitted

This webservice operation returns the EventId of the last XML-message that has validly been transmitted.

**Operation type:**  
Request-response. The endpoint receives a message, and sends a correlated message.

**SOAP action:**  
getLatestEvent

**Input:**  
GetLatestEventRequestMessage (soap:body, use = literal)

parameter type GetLatestEventRequest - extension of type  
RequestInformationType - extension of type RequestInformationType

Request in order to get the "EventId" of the last known XML-message of the casino that has been correctly transmitted to the FGB.

**Output:**  
GetLatestEventResponseMessage (soap:body, use = literal)  
parameter type GetLatestEventResponse

Response to the operation "getLatestEvent"

- LatestEvent - optional; type Event

Response is the "EventId" of the last known XML-message that has been correctly transmitted by the requesting casino. If no XML-messages have been transmitted so far by the requesting casino, the response is empty.

**Fault:**  
TemporarilyUnavailableFault (soap:fault, use = literal)  
fault type TemporarilyUnavailableInformation

Error message, if the webservice-interface is temporarily not available.

- ErrorMessage type string

Detailed error description

### 2. InsertEvents

**Description:**  
Delivery of XML-messages

This webservice operation delivers 1 to 50 XML-messages in one SOAP-message over the webservice-interface. All XML-messages have to be in the right order, with the first XML-message referencing the last XML-message that has validly been transmitted.

**Operation type:**  
Request-response. The endpoint receives a message, and sends a correlated message.

**SOAP action:**  
insertEvents

**Input:**  
InsertGameEventsRequestMessage (soap:body, use = literal)

parameter type InsertEventsRequest - extension of type RequestInformationType - extension of type RequestInformationType

Request for the operation InsertGameEvents

- GameEvent type Event

Collection of 1 to 50 XML-messages from the DSD for transmission over the webservice-interface.

**Output:**  
InsertGameEventsResponseMessage (soap:body, use = literal)  
parameter type InsertEventsResponse

Empty answer for transmission of XML-messages. Cf. InsertGameEvents.

- NumberOfImportedEvents type positiveInteger

Amount of received XML-messages. Corresponds to the amount of XML-messages in InsertGameEventsRequest.

**Fault:**  
EventValidationFault (soap:fault, use = literal)  
fault type EventValidationFailureInformation

Information concerning validation errors of XML-messages.

- Event type Event

The XML-message that could not be validated.

- ValidationFailureCode type EventValidationFailureCode - type string with restriction - enum { 'CORRECTED_EVENT_ID_NOT_FOUND', 'CORRECTED_EVENT_IS_CANCELLATION_EVENT', 'PREVIOUS_EVENT_ID_UNEXPECTED', 'PREVIOUS_EVENT_ID_MISSING', 'EVENT_HASH_MISSMATCH', 'EVENT_ID_EXISTS', 'SCHEMA_VALIDATION_FAILED', 'OTHER' }

Error code explaining the reason of failed validation.

- ErrorMessage - optional; type string

Error Message

**Fault:**  
TemporarilyUnavailableFault (soap:fault, use = literal)  
fault type TemporarilyUnavailableInformation

Error message, if the webservice-interface is temporarily not available.

- ErrorMessage type string

Detailed error description

## About wsdl-viewer.xsl

This document was generated by SAXON 9.1.0.8 from Saxonica XSLT engine. The engine processed the WSDL in XSLT 2.0 compliant mode.

This page has been generated by wsdl-viewer.xsl, version 3.1.01

Author: tomi vanek

Download at http://tomi.vanek.sk/xml/wsdl-viewer.xsl.

The transformation was inspired by the article  
Uche Ogbuji: WSDL processing with XSLT

This page was generated by wsdl-viewer.xsl (http://tomi.vanek.sk)