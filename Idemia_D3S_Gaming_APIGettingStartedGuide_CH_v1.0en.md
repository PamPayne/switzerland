---
country: Switzerland
document_name: D3S Developer’s Getting Started Guide - Web Services Integration - Switzerland
source_file: Idemia_D3S_Gaming_APIGettingStartedGuide_CH_v1.0en.pdf
extracted_date: 2026-04-30
jurisdiction: Switzerland
---

# D3S Developer’s Getting Started Guide - Web Services Integration - Switzerland

D3S Developer’s Getting Started Guide  
Web Services Integration - Switzerland  
D3S CH SAFE Server 5.0Functional Specification  
IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH  
Version 1.0 - 2018/11/22  
Reference : IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 1 of 10

Version : 1.0  
Date of latest update : 2018/11/22  
Related application version : 5.0  
Confidentiality : Restricted  
Audience Subject

## Revision list

| Version n° | Status (1) | Date | Author | Reason for / nature of update |
|---|---|---|---|---|
| 0.01 | P | 22/11/18 | Idemia | Creation |
| 1.0 | V | 23/11/18 | Idemia | Completion |

(1) P : in progress ; V : Validated

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 2 of 10

## Summary

1. INTRODUCTION......................................................................................................................................5  
1.1 Object of this document.......................................................................................................................5  
1.2 Special note for Portugal.....................................................................................................................5  
2 PRINCIPLES...........................................................................................................................................6  
2.1 Architecture.........................................................................................................................................6  
2.2 Environments.......................................................................................................................................6  
2.3 Web Service connection......................................................................................................................6  
2.4 WSDL convention................................................................................................................................7  
2.4.1 WSDL definition..............................................................................................................................7  
2.4.2 WSDL example...............................................................................................................................7  
2.5 XSD convention...................................................................................................................................8  
2.5.1 XSD definitions................................................................................................................................8  
2.5.2 XSD example..................................................................................................................................8  
2.6 Exception management.......................................................................................................................9  
2.6.1 UserFaultException.........................................................................................................................9  
2.6.2 SystemFaultException....................................................................................................................9  
2.7 Records passed as a list in all methods..............................................................................................9  
2.7 Uniqueness of idenfiants...................................................................................................................10  
2.8 Return value......................................................................................................................................10  
2.9 Idempotence......................................................................................................................................10  
2.9.1 Principles.......................................................................................................................................10  
2.9.2 Guidelines.....................................................................................................................................10  
3 ADDITIONAL DOCUMENTATION.............................................................................................................11

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 3 of 10

## 1. INTRODUCTION

### 1.1 Object of this document

The D3S SAFE Server software is a secure storage module enabling gaming applications to store records of gaming events. Typically, such events are needed for regulatory compliance. D3S implements the jurisdiction-specific requirements such as data formats, cryptographic seals, and communication protocols with the regulator.

This guide describes the communication API between the gaming application and D3S.

It contains 3 chapters:

- The present introduction chapter;
- Chapter 2 describes the general principles of use of the Web services;
- Chapter 3 point to additional information specific to the Web services for Switzerland.

### 1.2 Special note for Switzerland

The Swiss gaming regulator, the Federal Gaming Board (subsequently referred to as FGB) requires licensed operators to store a number of chained transactions in a Storage located in Switzerland called Data Storage Device (subsequently referred to as DSD). The data must be available to the FGB.

In addition, an application module called “WebService Client” by the FGB (and “Push Server” by IDEMIA) must push the data in near real time to the FGB Server.

IDEMIA’s D3S software and servers provide an architecture which complies with all the regulator’s requirements.

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 4 of 10

Gaming  
applicatio  
n

Gaming  
applicatio  
n

D3S

D3S

Regulator  
(FGB)

Regulator  
(FGB)

## 2 PRINCIPLES

### 2.1 Architecture

This documentation describes the WSDL  
1  
bindings that will be used to store gaming events for regulatory purposes.

This API is provided in a “Software as a Service” offer. It requires only that the gaming operator fulfills the security requirements (connection, privacy …) and provides correct information about players, gaming status and other notification at the right time.

SAFE Server services will then format, chain, calculate checksums, and store the corresponding event XML files in accordance with the regulatory rules.

The tracing methods are generic for all countries. But to fulfill regulatory requirements, per-country information are specified inside methods parameters, described in XML Schema data structure.

### 2.2 Environments

Three platforms are available:

- Integration platform: updated to latest version, this service will be maintained to enable adoption and debugging to new customer or during major updates;
- Load testing platform: we may open our load testing platform for customers which are looking for a production configuration dedicated to load balancing tests; load testing schedules must be agreed upon prior to the actual tests
- Production platform: backup, monitored, redundant, load-balanced, this platform is dedicated to our customers and real production environment. It must not be used for either functional or load tests, as records on this platform are published to the regulator

Please be aware that any record sent to the production platform will be handled as a real gaming event, and will be pushed to the FGB Server. Make sure to never send test data in production.

### 2.3 Web Service connection

The applications calling the Web services are authenticated at the D3S by X.509 certificate (SSL with mutual authentication) provided by IDEMIA.

The access control mechanisms of the D3S ensure that the source of a record is correctly authenticated and authorized through the SSL authentication certificate.

To specify the certificates using the following JVM parameters (replace brackets with ad hoc values):

- -Djavax.net.ssl.keyStore=\[path/to/your/certificate/yourCertificate.p12]
- -Djavax.net.ssl.keyStorePassword=\[passwordOfYourKeystore]
- -Djavax.net.ssl.keyStoreType=PKCS12
- -Djavax.net.ssl.trustStore=\[path/to/the/truststore/truststore.jks]
- -Djavax.net.ssl.trustStorePassword=\[passwordOfTruststore]

You can test your connection through the connect method of the “d3sc” command line tool that is available inside the SDK (See the README.txt file in the root directory of the provided archive).

1  
http://en.wikipedia.org/wiki/Web_Services_Description_Language

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 5 of 10

### 2.4 WSDL convention

#### 2.4.1 WSDL definition

The WSDL documents follow the given convention:

- filename: d3s-gaming-{PortName}-v1.wsdl
- namespace: http://idemia.com/ced/d3s/gaming/ch/service/{PortName}/v{V}.wsdl
- location: https://d3s.dictao.com/d3s/gaming/ch/service/{PortName}/v{V}\[u{X}]

The WSDL PortName can take one of the following values:

- realtime
- end-of-day
- eodaggreg
- echo

#### 2.4.2 WSDL example

The WSDL for the ports defines a port type with the following naming convention and methods:

{PortName}Port

writeRecords(List<Record> records): String

(echo is a specific case, and does not have a writeRecords method, but an echo method)

The port definition also defines the Record element, which is defined as a choice of different business elements. This way, it is possible to batch in a single web service call, records of various types pertaining to the same domain.

Record  
Choice  
{BusinessElement1}  
{BusinessElement2}  
...

The business types are defined in an XSD (see web services reference guide).

All web services calls on writeRecords return a unique string id for the call (safeCallId), assigned by the D3S Server, and allowing us to trace the call in the server logs.

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 6 of 10

### 2.5 XSD convention

#### 2.5.1 XSD definitions

The XSD documents corresponding to the ports follow the given convention:

- filename: d3s-gaming-{PortName}-v{YYYY_MM}.xsd
- namespace: https://idemia.com/d3s/jel/ch/service/{PortName}/v{YYYY_MM}.xsd

There are 2 schemas which do not correspond to a single web service port:

- The common schema, d3s-gaming-common-v{YYYY_MM}.xsd, contains various type definitions, used in the other xsds.
- The error schema, d3s-gaming-error-v1.xsd, contains the type definitions for the exceptions returned by the web services.

A web service port xsd defines the various business elements referenced in the wsdl’s method definition.

By convention, all business elements are the xml elements defined in the xsd.

#### 2.5.2 XSD example

Here is an example of definitions found in the XSD corresponding to the report port:

filename : d3s-gaming-end-of-day-v2018_12.xsd  
namespace: https://idemia.com/d3s/jel/ch/end-of-day/v2018_12.xsd

EndOfDay  
extension base=RecordBasicInfo  
sequence  
coveredDate  
record  
sequence  
depositTotal  
withdrawalTotal  
balanceTotal  
nonRedeemableBalanceTotal  
betTotal  
winningsTotal  
winningsTotalFromExternalJackpot  
jackpotIncrementTotalForExternalJackpot  
commissionTotalForExternalJackpot  
bonusTotalRealised  
betTotalFromExternalGame  
winningsTotalFromExternalGame  
taxes  
playersNumber

### 2.6 Exception management

All the methods can throw exceptions of two types specific to D3S and exposed by the WSDL:

- UserFaultException
- SystemFaultException

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 7 of 10

#### 2.6.1 UserFaultException

They are related to input data provided by the client. They contain an error code specified by the WSDL (file d3s-gaming-error-v1.xsd in folder /wsdl/ch/v1).

These exceptions corresponding to problems related to user data, the client application should catch them as it should know how to handle them (modify input data; inform the end user, etc). Choice should be based on the interpretation of the exception code. In any case the client application must not resend this data without correcting it first, or correcting the connection (especially in case of missing privilege, invalid certificate…).

A safeCallId is returned as part of the structure, which the client application should log in case you need IDEMIA to investigate if the SAFE Server has more information about the error than what the client application was able to capture.

The D3S server remains operational; it just needs correct input data to provide its services.

Example: invalid input data, like a violation of unique constraint

#### 2.6.2 SystemFaultException

They are related to the execution environment of the D3S.

The client application should log the error and the safeCallId. The safeCallId will be required if and when you need IDEMIA to investigate this specific error instance.

These exceptions corresponding to problems on the environment, such as network connectivity, the client application should try again later. A recommended approach, in order to flood a busy SAFE Servers with numerous retries, is to use the “exponential backoff” algorithm, which gradually delays the retries.

Return to a normal service of D3S is usually very quick, thanks to the SAFE Server’s high availability architecture. If the problems lies with a single instance, our load balancer will redirect the future calls to the more available instance. If the problems lies in network connectivity problems, the issue will usually disappear in a short time frame.

### 2.7 Records passed as a list in all methods

The method writeRecords takes a list of records as input. This allows processing multiple orders in a single network round trip.

The maximum number of instances in a single call is limited to 1000 or 2Mbytes of data, whichever comes first.

### 2.7 Uniqueness of idenfiants

Every record send has a XML-element called “recordId”. The value of this XML-element must be unique. IDEMIA recommends the use of a GUID (in the form xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, where x is a lower case hexadecimal digit) as value.

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 8 of 10

### 2.8 Return value

When a web service call succeeds, that is when no exception is thrown during the call, the server returns a single String value. This value represents an id assigned by the server to the call (since a call may store several records at once in the SAFE Server, this safeCallId may concern several records and may not be considered as a recordID). The client application should log it for reference, as it may be used to track some information in the server logs.

This id represents the acknowledgement that the server received the data, and that it takes the responsibility of processing it and making it available to the regulator according to their specifications.

### 2.9 Idempotence

#### 2.9.1 Principles

The server implements a mechanism to avoid processing multiple times the same records sent repeatedly though asynchronous calls (to the writeRecords method), thus ensuring the web service idempotence (http://en.wikipedia.org/wiki/Idempotence).

Therefore, in any case you have no way to know that your call was received by the D3S server, you should carry out the same call again until you get a response (either an Exception, or a return value).

The idempotence function has the following characteristics:

- There is one history cache per operator.
- The cache keeps record references for one month. Therefore a record sent a second time more than one month after the original record was sent will not be detected and will be processed by the safe.
- A record is identified by all its content, as defined by the regulator. A record sent with a different value for even just one field will be processed a second time.

#### 2.9.2 Guidelines

Only by following the guidelines below can we make sure there are no duplicates in the safe.

- If you want to retry sending a record, don’t delay too much before retry it; after one month, it will be too late.  
  If you resend a record after 1 month, the record of the original call will be out of the cache and the retry will not be caught as a repetition.
- If you want to resend a record that you are not certain it was sent to the SAFE server, do it with exactly the same field values;  
  If you change anything in a record, the safe will flag it as a different record, and it will be made available to the regulator.

## 3 ADDITIONAL DOCUMENTATION

A reference guide is available with the development kit. It describes in details the various elements and types used in the web services.

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 9 of 10

The development kit itself is a good place to start in order to get familiar with the web services. It contains examples of how to use the different web services calls, and demonstrates with simple use cases the type of data expected for each calls.

A use case documentation is available on IDEMIA’s Switzerland web site for partners (https://i-sphere.fr/sites/DSA/online-gaming-switzerland).

If you have any questions about the use cases you can send your questions at sec.ilm.dsa.gaming-compliance-ch@idemia.com. For questions about the web services and how to integrate with our server you can send your questions at sec.ilm.dsa.gaming-integration@idemia.com. We will make sure to respond promptly.

Ref.: IDEMIA_D3S_Gaming_APIGettingStartedGuide_CH Version 1.0 2018/11/22  
Communication, reproduction and use restricted to the purpose of this document Page 10 of 10