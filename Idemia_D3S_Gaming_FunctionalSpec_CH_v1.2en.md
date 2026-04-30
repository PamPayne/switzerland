---
country: Switzerland
document_name: D3S Gaming Functional Specification - Switzerland Regulation
source_file: Idemia_D3S_Gaming_FunctionalSpec_CH_v1.2en.pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# D3S Gaming Functional Specification - Switzerland Regulation

## Document Information

**D3S Gaming Functional Specification**

Switzerland Regulation

D3S Gaming Switzerland 5.0 Functional Specification

Idemia_D3S_Gaming_FunctionalSpec_CH

Version 1.0 - 2019/02/18

Reference: Idemia_D3S_Gaming_FunctionalSpec_CH  
Version: 1.0  
Date of latest update: 2019/02/18  
Related application version: 5.0  
Confidentiality: Restricted

### Revision list

| Version n° | Status (1) | Date | Author | Reason for / nature of update |
|---|---|---|---|---|
| 0.01 | P | 16/11/18 | Idemia | Creation |
| 1.0 | V | 01/12/18 | Idemia | Completion |
| 1.2 | V | 18/02/19 | Idemia | Completion |

(1) P : in progress ; V : Validated

## Summary

1. INTRODUCTION  
1.1 Object of this document  
1.2 Targeted audience  
1.3 External references  

2 REQUIREMENTS OVERVIEW  
2.1 Definitions  
2.1.1 Data Storage Device (DSD)  
2.2 General Regulatory Requirements  
2.2.1 Regulator Data model  
2.2.2 Requirements on DSD data  
2.2.3 Webservice Client  
2.2.4 Homologation  
2.2.5 DSD Location  
2.2.6 Time zone  
2.3 Functional Regulatory Requirements  
2.3.1 Authentication  
2.3.2 Near real-time  
2.3.3 Event Types  
2.3.4 Event Data Model  
2.3.5 Unique Identifier of Events  
2.3.6 Data chaining  
2.3.7 Data integrity  
2.3.8 End of day authenticity  
2.4 Misc. Requirements  
2.4.1 Backup Strategy  
2.4.2 Redundancy  
2.4.3 Retention Period  

3 PRODUCT FUNCTIONS  
3.1 Architecture Overview  
3.1.1 D3S High-Level Functional Flow  
3.1.2 Usage Statistics  
3.1.3 Synchronous vs Asynchronous  
3.2 Web Service Front-end  
3.2.1 Overview of the Recording API  
3.2.2 WSDL and SOAP format  
3.2.3 Synchronous two-way  
3.2.4 Fault Handling  
3.2.5 Services Exposed for the Switzerland SAFE  
3.2.6 Duplicated Requests Detection  
3.2.7 Request Context  
3.3 User Authentication  
3.3.1 Transport Layer Security  
3.3.2 User Directory  
3.3.3 Authentication Context  
3.4 Validation & Transformation  
3.4.1 SOAP Body Validation  
3.4.2 IDEMIA XML vs FGB XML  
3.5 Dispatching  
3.5.1 Dispatch Logic  
3.5.2 Asynchronous Queuing  
3.6 Batch Management  
3.6.1 Purpose of batch  
3.6.2 Batching Rules  
3.7 Timestamping  
3.8 Compression  
3.8.1 Compression Characteristics  
3.9 Directory and File Management  
3.9.1 Directory Structure  
3.9.2 Batch Files  
3.9.3 Receipt ZIP Files  
3.9.4 Rejected ZIP Files  
3.9.5 Log Files  
3.9.6 Error Log Files  
3.10 Regulatory Read Access  
3.10.1 File Download  
3.10.2 Directory Browsing  
3.11 Operator Read Access  
3.12 Sanity checks  
3.12.1 Sanity check at startup  
3.12.2 Recovery mechanism of sending data to FGB  

4 DATA MODEL MAPPING RULES  
4.1 General Principles  
4.2 Conversions

## 1. INTRODUCTION

### 1.1 Object of this document

The D3S SAFE Server software is a secure storage module enabling gaming applications to store records of gaming events. Typically, such records are needed for regulatory compliance.

D3S implements the jurisdiction-specific requirements such as data formats, cryptographic seals, and communication protocols with the regulator.

This document is the functional specification of the D3S SAFE Server for the Online Gaming in the Switzerland jurisdiction.

It describes the SAFE regulatory requirements established by the Federal Gaming Board (FGB) and how these requirements are fulfilled by the D3S software.

### 1.2 Targeted audience

This document is primarily intended to:

- Idemia R&D teams that develop, test and deliver the D3S software product,
- Idemia Administration & Support teams that operate the product as a service (SAAS).
- External certification teams that evaluate the software product with regard to the Gambling Act requirements.

### 1.3 External references

- Ordinance on money games (OJAr of 07 November 2018): https://www.ejpd.admin.ch/dam/data/bj/wirtschaft/gesetzgebung/geldspielgesetz/vgs-f.pdf
- FDJP Ordinance on gambling houses (OMJ-DFJP of 07 November 2018): https://www.ejpd.admin.ch/dam/data/bj/wirtschaft/gesetzgebung/geldspielgesetz/spbv-ejpd-f.pdf

## 2 REQUIREMENTS OVERVIEW

### 2.1 Definitions

#### 2.1.1 Data Storage Device (DSD)

**Data Storage Device (DSD)** The “Article 60 of Ordinance on money games (OJAr of 07 November 2018)” and the “Article 39 of FDJP decree on gambling houses (OMJ-DFJP of 07 November 2018) define the Data Storage Device (DSD) as the mandatory system for the online gambling operators. It must contains all the data for each gaming session.

### 2.2 General Regulatory Requirements

#### 2.2.1 Regulator Data model

The information extracted from the gaming online system shall be archived following the regulator (FGB) data model in the DSD to which the FGB shall be provided permanent access.

#### 2.2.2 Requirements on DSD data

- Integrity: it must be possible to verify no data has been altered afterwards;
- Authenticity: it must be possible to verify the data was really written at the indicated time;
- Completeness: it must be possible to detect, if the data has been deleted afterwards.

#### 2.2.3 Webservice Client

The Webservice Client is also responsible to send the gambling related data stored in DSD to the FGB server.

We will call it in the rest of the document “Push server”.

#### 2.2.4 Homologation

During the homologation process, the operator must obtain a unique identifier for each type of authorized games.

#### 2.2.5 DSD Location

According to the “Article 60 of Ordinance on money games (OJAr of 07 November 2018)”, the DSD must be on the Switzerland.

#### 2.2.6 Time zone

All date and time in the XML record stored in the DSD must use the official time in Switzerland.

### 2.3 Functional Regulatory Requirements

#### 2.3.1 Authentication

The Article 39 of FDJP decree on gambling houses (OMJ-DFJP of 07 November 2018) does not define the specific means of authenticating for access to the DSD.

However, the FGB agreed with accessing the DSD data over HTTPS and using a login/password scheme.

#### 2.3.2 Near real-time

The various transactional events (games, payments) must be recorded into the DSD after completion of an individual transaction.

This means that the recording of those events is near real time, and for all practical purposes has to be carried out within a few minutes of the actual event completion (other regulations typically allow up to five minutes delay).

#### 2.3.3 Event Types

Recorded events include the following category of information:

- Transaction events (bonus conversion / transfer, player status, player payment, casino payment, tax): The transaction records are a family of 6 derived message types storing transactions to or from a player's account:
- Game session events
- Jackpot events
- Cancellation events
- End of day events

#### 2.3.4 Event Data Model

The events that the Webservice client sends to the FGB server (near-real time events, transactions, game session, jackpot, …) must be encoded into XML document that conform to the XSD schema published by the FGB. The namespace for the xml schema is “http://ejpd.admin.ch/esbk/services/casino-events/v1”.

#### 2.3.5 Unique Identifier of Events

The FGB defines for each XML data in DSD a unique identifier “EventId” witch can be a subsequent number or an UUID.

The APIs exposed by D3S Server for submitting events have a XML-element "recordID". This element corresponds to XML-element "eventId" defined by the regulator. The gaming operator must ensure that the value of the "recordID" in the event it wants to submit is unique.

IDEMIA recommends the use of a GUID (in the form xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, where x is a lower case hexadecimal digit).

#### 2.3.6 Data chaining

The data stored in the DSD must be chain to detect missing or deleted data.

Each XML data holds the “EventId” and the hash of its predecessor (calculated upon creation of the predecessor) and to form a chain of XML-messages.

#### 2.3.7 Data integrity

Each XML event is hashed with the SHA-1 algorithm and the calculated hash value is subsequently added to the XML-message in hexadecimal representation and stored in the DSD.

#### 2.3.8 End of day authenticity

The end of day event, due to be generated every day after midnight, carries a field for a crypto-timestamp according to RFC3161.

### 2.4 Misc. Requirements

#### 2.4.1 Backup Strategy

The data recorded into the DSD are stored in two physical locations:

- A primary site (in Switzerland)
- A backup site (in France)

#### 2.4.2 Redundancy

In order to achieve the required high availability, several D3S Server can be setup and running concurrently. The gaming operator capture device sends the events in any one of them at a given time.

#### 2.4.3 Retention Period

According to the “Article 61 of Ordinance on money games (OJAr of 07 November 2018)”, the DSD must keep the data for a minimum period of 5 years.

## 3 PRODUCT FUNCTIONS

### 3.1 Architecture Overview

#### 3.1.1 D3S High-Level Functional Flow

The diagram below illustrates the functional flow of the D3S Solution for Switzerland.

The functional flow is as follows:

1. The D3S Server listens for incoming remote request. The messaging and transport protocol is SOAP over HTTPS.
2. Whenever a new request arrives, the D3S Server first authenticates the request imitator. The authentication is based upon the standard Transport Layer Security (TLS) protocol with mutual X509 certificate authentication.
3. The SOAP message goes through a validation layer.
4. The individual XML event goes through a transformation layer. The XML events in SOAP body are parsed and converted to individual FGB XML event. All the date time elements in XML events are converted to Switzerland time zone.
5. Each individual XML event goes through a dispatching processor which forwards the record to the appropriate batch queue. The dispatching logic is based upon the execution context (authenticated operator, record type…). The SOAP response is then returned to the caller (gaming operator), and the event will be processed asynchronously.
6. Multiple individual FGB XML records are grouped together in a batch. In effect, batches are limited to 50 records and have a maximum timespan of 30 minutes. The maximum limit of 50 corresponds to the maximum number of events that can be sent to the FGB in a single call through the webService Client.
7. Each batch is compressed using the zip algorithm into a file named data.zip
8. Each ZIP file is written onto the disk as it is produced by the system. The files are stored following a strict folder structure and naming convention. The layout is based upon the context (operator sending the event, vault processing the event, time…).
9. The Push Server (WebService Client) picks up new batches on the disk and:
   a. The Push Server verify the completeness and the integrity of the last chained event with its previous event. The previous event is searched using the previsousEventId field in the last chained event. Then the Hash of the previous event is recalculated and compared to the field previousEventHash on the last chained event.  
   b. The Push Server performs the chaining of the FGB XML of the batch by using the date of writing on the disk. Each individual FGB XML in the batch are modified and the fields “PreviousEventId” and “PreviousEventHash” are set;  
   c. The Push Server calculates the checksum for each individual FGB XML in the batch using the SHA-1 hash algorithm. The SHA-1 value is stored in the same XML in the field “EventHash” according to the regulation rules;  
   d. For only the end-of-day XML, the Push Server calculates a crypto-timestamp. The crypto-timestamp value is stored in the same end of day XML (field “CryptoTimestamp”);  
   e. The Push Server writes the new batch containing the chained events into the DSD. The zip batch are stored following a strict folder structure and naming convention. The zip batch is read protected by a specific password for the operator;  
   f. The Push Server moves the old batch to temporary folder on the disk. This temporary folder is empty regularly.
10. The Push Server picks up the new chained batches on DSD and:
   a. The Push server sends the chained batches to the FGB Server in a single call;  
   b. The Push server logs the attempts and outcomes of each call into the DSD following a naming convention.
11. The data in the DSD in France are periodically replicated in the Switzerland’s DSD. In the fact the data is replicated every 10 minutes.
12. The FGB can access to the Swiss DSD in HTPPS from an internet browser.

#### 3.1.2 Usage Statistics

The D3S Server functional flow is monitored at the different stages ofthe processing, including

- The number of requests per second received on average and peak time,
- The min, max and average request size,
- The min, max average clear form and compressed batch,
- The average daily storage growth per operator,
- The usage statistics for billing.

#### 3.1.3 Synchronous vs Asynchronous

The functional flow is divided in two parts:

1. The first part is synchronous. It includes the operations 1 to 5 (SOAP request handling, authentication, transformation and dispatch).
2. The second part is asynchronous. It includes all the remaining operation 5 to 11 (batch, hashing / timestamping process, chaining process, submission to the FGB , store)

The synchronous operations are executed within the thread handling the incoming SOAP request. The gambling operator system sends the request and waits until it received a response for the D3S. The caller thread is blocked while the call is being processed. The D3S returns a status indicating whether the request was valid or not.

The D3S executes the first 4 operations synchronously in order to fully validate the incoming request as follows:

- It validate that the SOAP message in well-formed. If validation fails, it returns an error immediately.
- It authenticates the Capture Device. If the X509 certificate is unknown, it returns an error immediately.
- It validates and transforms the body to an individual FGB XML. If the validation or transformation fails, it returns an error immediately.
- It interprets the relevant part of the FGB event, and dispatches it to the right batch queue. If the dispatch is not authorized for the authenticated operator, it returns an error immediately.

By design, once all these operations have been completed successfully, the D3S knows that it will be able to complete the remaining operations successfully. Consequently, it returns immediately a success status code and proceeds with the remaining operations asynchronously.

### 3.2 Web Service Front-end

#### 3.2.1 Overview of the Recording API

The D3S Server exposes its recording API via Web service endpoints using SOAP over HTTPS. All endpoints are fully described by a WSDL document that is provided statically within a development kit.

#### 3.2.2 WSDL and SOAP format

A WSDL document describes the how the service is bound to a specific SOAP message protocol. Several options exist in the standard, namely RPC and document binding with either encoding or literal body.

The D3S WSDL uses a document/literal style with request/response wrapped. The style is illustrated below:

<types>  
<schema>  
<element name="myMethod">  
<complexType>  
<sequence>  
<element name="firstname" type="xs:string"/>  
<element name="lastname" type="xs:string"/>  
</sequence>  
</complexType>  
</element>  
<element name="myMethodResponse">  
<complexType>  
<element name="returnValue" type="xs:int"/>  
</complexType>  
</element>  
</schema>  
</types>  
<message name="myMethod">  
<part element="myMethod" name="input" />  
</message>  
<message name="myMethodResponse">  
<part element="myMethodResponse" name="output" />  
</message>  
<portType name="PT">  
<operation name="myMethod">  
<input message="myMethod"/>  
<output message="myMethodResponse"/>  
</operation>  
</portType>

The SOAP message sent over the wire is illustrated below

<soap:envelope>  
<soap:body>  
<myMethod>  
<firstname>john</firstname>  
<lastname>doe</lastname>  
</myMethod>  
</soap:body>  
</soap:envelope>

With this style, the XML element defined in the SOAP body can be validated against an XSD schema.

The WSDL is slightly more complex than a regular document/literal binding, where the element “myMethod” and “myResponse” don’t exist. However, this style is broadly used and recent Web service tooling (JAXWS for Java, WCF for .NET and more) detects this pattern and hides these intermediates elements in the generated code they produce as illustrated below

int myMethod(String firstname, String lastname)

#### 3.2.3 Synchronous two-way

All methods defined in the recording API are both synchronous and two-way.

- The caller sends a request over HTTP and waits for the HTTP response,
- The D3S Server receive the request, executes it and write the response synchronously,
- The caller receives the HTTP response (success or failure) and acts accordingly.

#### 3.2.4 Fault Handling

When the D3S encounters an unexpected condition (invalid caller request, resource missing, unexpected condition), it returns a SOAP fault to the caller.

Faults are classified in 2 main categories:

- UserError: the caller request is invalid and should be fixed on the caller side. The same request must not be resent to the D3S Server.
- SystemError: the D3S system has encountered an unexpected condition. The same request might be resubmitted to the D3S once the malfunction is fixed.

#### 3.2.5 Services Exposed for the Switzerland SAFE

All services calls are made through a single method, writeRecords, which takes a heterogeneous list of records allowed for the service, and returns the D3S Server generated call Id.

#### 3.2.6 Duplicated Requests Detection

The availability of the Web service API relies upon the underlying network layer. In general, the API is in one of the following states:

- The network is up: requests and responses are processed successfully,
- The network is down: requests fail before they reach the D3S Server.

In those situations, no extra care needs to be taken: requests are either fully processed or not processed at all.

There is one situation that needs special care: if the network goes down while a request is being processed, the request might have been fully executed by the D3S but the response never reach the caller. The caller will probably submit the request again, which will eventually be received by the D3S Server and executed a second time.

In order to prevent these duplicate requests, the D3S uses the following duplicate detection protocol:

- The first time a call is made, a hash (SHA1) of the incoming web service message is computed, the message is processed and stored in the vault, and the hash is stored in a cache along with the response
- When a network error occurs, the caller retries sending the same request.
- The D3S Server computes the hash on the incoming message, finds a match in the cache, does not process or store the new message, but sends the success response back.
- In order to control the cache growth, the cache is limited to 20000 entries.

Special provisions for calls:

- An additional mechanism is put in place that prevents duplicates at the record level. Each record, prior to being added to a batch, is checked against a record database containing a hash of the FGB xml document. The cache maintains one month of records. If a document was found to have been already submitted, it is discarded from the batch.
- Due to the existence of the much stronger record level duplicate checking, the call level duplicate verification does not have to be as strong as for the synchronous calls. We do maintain it, however, to prevent flooding with repeated call, and spare the server extra processing. In this case the cache is in memory only (per D3S instance), and limited to 100 entries per user certificate used to authenticate with the safe.

#### 3.2.7 Request Context

A request context is allocated and populated with the IP address of the requester and forwarded to the next operation.

### 3.3 User Authentication

#### 3.3.1 Transport Layer Security

The D3S Server implements the standard security protocol “Transport Layer Security” (TLS) to secure the incoming SOAP requests and outgoing SOAP responses.

TLS is a client-server protocol that fulfills the following objectives:

- Server authentication,
- Client authentication,
- Integrity and confidentiality of exchanged messages.

The authentications are based upon X509 certificates that are issued by known and trusted CA on both ends.

#### 3.3.2 User Directory

Once the TLS channel has been established between the caller and the D3S Server, the vault gets the SSL X509 certificate of the caller.

From that point, the vault:

- Extracts the Issuer DN (DN of the trusted CA that issued the certificate),
- Extracts the Subject DN (DN of the caller’s certificate itself),
- Looks up if the user key pair {IssuerDN+SubjectDN} exists in the user directory.

The user directory associates the user key pair {IssuerDN+SubjectDN} with a set of rights and configuration parameters. This directory is managed by the D3S administrators.

- If the pair exists, the configuration and rights are loaded into the vault and associated to the incoming request.
- If the pair doesn’t exist, the D3S Server returns an error immediately.

#### 3.3.3 Authentication Context

An authentication context is allocated and populated with the parameters retrieve from the user directory and forwarded to the next operation.

### 3.4 Validation & Transformation

#### 3.4.1 SOAP Body Validation

As specified in the Web service section, the Web service WSDL follows the encoding style document/literal. This style ensures that all messages in the SOAP body are defined in a XSD document.

As such, the XML can be fully validated against an XSD schema.

#### 3.4.2 IDEMIA XML vs FGB XML

Before being stored, the XML records must go throw different steps including:

1. Capturing the actual information ultimately stored in the XML,
2. Sending the information between the different subsystems up to the vault,
3. Formatting the information in the FGB XSD compliant format.

The FGB XSD schema defines the structure of the XML document stored onto the file system and sending to the FGB, which will eventually be uploaded and interpreted by the regulator.

IDEMIA has defined its own XSD that address these issues:

- The IDEMA XSD is in well documented, in English,
- The IDEMIA XSD can hide structural changes in the FGB XSD,
- The IDEMIA XSD is fine grain, defining individual element that can be computed where the data are captured.
- The IDEMIA XSD is capture centric, along with the WSDL document, it precisely defines what, when and how data are sent to the vault.

The D3S Server implements its own transformation engine. XML records sent to the vault in the IDEMIA XML format are transformed in the FGB XML format transparently. The data model mapping is specified in section “4- Data Model Mapping Rules”.

### 3.5 Dispatching

#### 3.5.1 Dispatch Logic

The dispatching logic determines the destination of individual FGB XML records.

To that end, it uses the different contexts populated in the previous stages:

- Request context,
- Authentication context,
- And the content of the individual FGB XML elements transformed in the previous stage.

#### 3.5.2 Asynchronous Queuing

For each operator, the D3S Server maintains a persistent queue of batches to be produced.

Once the dispatch logic has completed, the XML record is pushed into one of those queues.

The synchronous processing is completed. The remaining operations will be executed asynchronously, getting XML events from the queues.

### 3.6 Batch Management

#### 3.6.1 Purpose of batch

A batch is used to group records together.

A batch corresponds to one file on the file system; it has an identifier that must be unique for a given digital safe and operator. This identifier is a short integer, whose unicity is ensured by the D3S server.

#### 3.6.2 Batching Rules

Batches must be generated according to the following rules:

- End of day calls records are batched separately from other events calls.
- A new batch is closed and saved to the disk:
  - When the amount of time that has elapsed since the first record in the batch was received reaches 30 minutes.
  - When the total number of records in the batch reaches or exceeds 49.
  - When a batch is open, non-empty, and the time of day reaches midnight Europe/Geneva.

### 3.7 Timestamping

The end of day events are time stamped according to the RFC3161 standard.

### 3.8 Compression

#### 3.8.1 Compression Characteristics

For each new batch, a zip file is created.

The individual XML record are marshaled and stored as UTF-8 into a byte array. Each XML file is added as a new entry in the zip file with the byte array content.

The zip batch file is read protected by a password. This password is specified for each operator.

### 3.9 Directory and File Management

#### 3.9.1 Directory Structure

The directory structure is created at run-time by the Push server, following best practices used in other regulations.

- OPERATOR
  - data
    - YYYY
      - MM
        - DD
          - OPERATOR_rec_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip
          - OPERATOR_eod_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip
          - OPERATOR_rec_YYYYMMDDHHMMSS_BATCHGUID.zip
          - OPERATOR_eod_YYYYMMDDHHMMSS_BATCHGUID.zip
  - receipts
    - YYYY
      - MM
        - DD
          - OPERATOR_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip
          - OPERATOR_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip
  - rejected
    - YYYY
      - MM
        - DD
          - OPERATOR_YYYYMMDDHHMMSS_EventID_BATCHGUID.zip
          - OPERATOR_YYYYMMDDHHMMSS_EventID_BATCHGUID.zip
  - errlogs
    - dictao-d3s-oper.YYYY-MM-DD.log
  - logs
    - dictao-d3s-fgb.YYYY-MM-DD.log
    - dictao-d3s-perf.YYYY-MM-DD.log

The OPERATOR name is specified in the D3S configuration; all other directories names are computed by the D3S.

The structure exposed to the monitoring authority through the HTTPS server only exposes the content starting with OPERATOR at the root.

The same structure is available to the operator through the HTTPS server. This connection is protected by login/password and by client IP whitelisting.

#### 3.9.2 Batch Files

The files are created and written down at run-time by the Push srv, under the data folder, using the following convention for batches that have already sent to FGB Server:

- OPERATOR_rec_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip: it contains all types of events except end of day events. The first date time is the created date on the DSD. The second date time is the date of sending to FGB Server.
- OPERATOR_eod_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip: it contains only the end of day events. The first date time is the created date on the DSD. The second date time is the date of sending to FGB Server.

And the following convention for batches that have not yet been sent to FGB Server:

- OPERATOR_rec_YYYYMMDDHHMMSS_BATCHGUID.zip: it contains all types of events except end of day events. The date time is the created date on the DSD. When the batch is successful sent to FGB the batch is renamed to OPERATOR_rec_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip with the date of sending to FGB Server.
- OPERATOR_eod_YYYYMMDDHHMMSS_BATCHGUID.zip: it contains only the end of day events. The date time is the created date on the DSD. When the batch is successful sent to FGB the batch is renamed to OPERATOR_eod_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip with the date of sending to FGB Server.

The OPERATOR name is specified in the D3S configuration; all other parts are computed by the Push server.

- BATCHID: a GUID uniquely identifying the batch (in the form xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, where x is a lower case hexadecimal digit).

#### 3.9.3 Receipt ZIP Files

The files are created and written at run-time by the Push Server. Each receipt file corresponds to a single batch file bearing the same name, and placed in the receipts folder with the same YYYY/MM/DD subdirectory structure.

- OPERATOR_rec_YYYYMMDDHHMMSS _YYYYMMDDHHMMSS_BATCHGUID.zip
- OPERATOR_eod_YYYYMMDDHHMMSS _YYYYMMDDHHMMSS_BATCHGUID.zip

The receipts batch file is a zip containing the SOAP request response of FGB server. This response corresponds to the single acknowledgment of registration of the all events in the batch on the FGB Server. It contains an XML file:

- Response_ BATCHGUID.xml

In addition, in case the FGB server returns a TemporarilyUnavailableInformation response, meaning “retry later”, the responses to the failed attempts are stored in the zip under the errors folder:

- errors
  - response-M.xml

In the name above M is the failed attempt number, starting with 1.

#### 3.9.4 Rejected ZIP Files

The files are created by the Push Server when the FGB server rejects the submission of events.

Several cases of rejection of an event are defined in the regulation:

- when the XML-element "EventId" in one event in the batch does already exist in the database of the FGB.
- When a cancellation event cancels another cancellation event.
- When the XML-element "PreviousEventId" in one event references an event which is unknown or is not the last XML-message transmitted to FGB Server.
- When XML-element "PreviousEventId" in one event is omitted and it is not the very first XML-message of the transmitting to FGB Server.
- Etc.

In the fact, only the first error can happen.

#### 3.9.5 Log Files

Under the logs folder are the log files, listing all attempts to send a batch to the FGB server, and all outcomes.

Those files are rotated daily.

This folder contains files:

- dictao-d3s-fgb.YYYY-MM-DD.log: This is the log file containing the transaction information to the FGB Server made by the Push server.

In addition, this folder contains the performance logs, which allow to detect a latency of the sending on the FGB server FGBmeaning:

- dictao-d3s-perf.YYYY-MM-DD.log:

Note that unlike the zip files, the log files’ YYYY-MM-DD follows the Switzerland time.

#### 3.9.6 Error Log Files

Under the errlogs folder are stored the logs files containing one line per batch that the FGB Server rejected upon submission by the Push Server.

The operator will need to check those files regularly, as the rejected records will generally need to be corrected and resubmitted to the D3S server.

The files are rotated daily and their name follows this pattern:

- dictao-d3s-oper.YYYY-MM-DD.log

Note that unlike the zip files, the log files’ YYYY-MM-DD follows the Switzerland time.

### 3.10 Regulatory Read Access

#### 3.10.1 File Download

All files in the DSD can be downloaded individually using the HTTP GET request (through the HTTPS protocol, with login and password).

In particular the batch ZIP files downloaded individually using the HTTP GET request.

A file can be downloaded as follows:

- A request line GET /PATH
- Which request the file specified in the PATH
- The PATH is relative to the OPERATOR root directory as follows:
  - OPERATOR_rec_YYYYMMDDHHMMSS_YYYYMMDDHHMMSS_BATCHGUID.zip

The server response content type depends upon the nature of the file being downloaded.

- ZIP file content type is « application/zip »

#### 3.10.2 Directory Browsing

In order to ease the burden of browsing and downloading file for a human being, the D3S provides a simple directory browsing facility.

A directory can be listed using the HTTP GET request.

- A request line GET /PATH
- Which list the contents of the directory specified in the PATH
- The PATH must be terminated by a slash ‘ /’ to trigger the listing on the server side as follows:
  - /OPERATOR/data/YYYY/MM/DD/

The server response is a simple HTML file that list the available subdirectories or files as hyperlink <a href>.

### 3.11 Operator Read Access

A read access is also provided to the owner of the safe. The URL and login/password is specific to the gaming operator.

The same URLs to browse the safe or download the files are available, however, the /OPERATOR part must be omitted, as only one safe is available to a given gaming operator.

### 3.12 Sanity checks

Sanity checks should be performed by the push server in order a have healthy vault.

#### 3.12.1 Sanity check at startup

At startup, the push server will perfume a sanity check for all batch files in the vault. Integrity, authenticity and completeness will be verified for each chained batch files:

- Authenticity: validate timestamp of each eod
- Integritiy: validate hash = hash (record - 1)
- Completeness: validate previousEventID(record) = EventID (record -1)

#### 3.12.2 Recovery mechanism of sending data to FGB

The pushSrv must transmits every message without delay to the FGB, whenever the webservice-interface is up and running. In case the webservice interface should be down, operation can continue and the data is to be stored as before as XMLmessage in the DSD.

When the webservice-interface is up and running again, transmission of the XMLmessages to the regulator server has to resume with the last XML-message that could not be sent.

We can use the call to regulator server getLastMessage in order to make sure what is the latest recordID successfully transmited to regulator.

## 4 DATA MODEL MAPPING RULES

### 4.1 General Principles

The D3S Server converts the IDEMIA data model into the FGB data model synchronously during the web service call to the Server. This allows D3S to validate that the resulting data is conformant in every respect to the XSD provided by the regulation authority.

In addition to converting the data, D3S injects some information corresponding to the Safe system in accordance to the regulation.

### 4.2 Conversions

The D3S does convert:

- A IDEMIA XML element into a FGB XML element,
- A simple IDEMIA XML element into a FGB XML attribute,
- A IDEMIA XML attribute into a FGB XML attribute or element,
- Some enumeration values from the IDEMA XML into corresponding enumeration values described in the FGB XML schema,
- Some enumeration values from the IDEMIA XML into free text values in the FGB XML,
- Timestamps values from their canonical representation to their specific representation and time zone in the FGB xml document.

D3S will not alter the free text information provided by the gaming system. It will be passed untouched into the corresponding element or attribute in the FGB XML document.