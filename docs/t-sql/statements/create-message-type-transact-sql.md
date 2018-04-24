---
title: CREATE MESSAGE TYPE (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 04/10/2017
ms.prod: sql
ms.prod_service: sql-database
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_MESSAGE_TSQL
- MESSAGE_TSQL
- MESSAGE
- CREATE MESSAGE
- CREATE_MESSAGE_TYPE_TSQL
- MESSAGE TYPE
- MESSAGE_TYPE_TSQL
- CREATE MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- XML [Service Broker]
- validation [Service Broker]
- message types [Service Broker], creating
- empty messages [SQL Server]
- binary [SQL Server], message types
- CREATE MESSAGE TYPE statement
ms.assetid: 98fe0fff-1a2e-4ca2-b37f-83a06fdf098e
caps.latest.revision: 41
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 67a5149692017533f2941770f39088871b2b389e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="create-message-type-transact-sql"></a>CREATE MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Erstellt einen neuen Nachrichtentyp. Mit einem Nachrichtentyp wird der Name einer Nachricht und die Überprüfung festgelegt, die [!INCLUDE[ssSB](../../includes/sssb-md.md)] für Nachrichten mit diesem Namen ausführt. Auf beiden Seiten einer Konversation müssen dieselben Nachrichtentypen definiert sein.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
CREATE MESSAGE TYPE message_type_name  
    [ AUTHORIZATION owner_name ]  
    [ VALIDATION = {  NONE  
                    | EMPTY   
                    | WELL_FORMED_XML  
                    | VALID_XML WITH SCHEMA COLLECTION schema_collection_name  
                   } ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumente  
 *message_type_name*  
 Der Name des Nachrichtentyps, der erstellt werden soll. Ein neuer Nachrichtentyp wird in der aktuellen Datenbank erstellt, sein Besitzer ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. *message_type_name* kann aus bis zu 128 Zeichen bestehen.  
  
 AUTHORIZATION *owner_name*  
 Legt den Besitzer des Nachrichtentyps auf den angegebenen Datenbankbenutzer oder die angegebene Datenbankrolle fest. Ist der aktuelle Benutzer **dbo** oder **sa**, kann *owner_name* der Name eines beliebigen gültigen Benutzers bzw. einer beliebigen gültigen Rolle sein. Andernfalls muss *owner_name* der Name des aktuellen Benutzers, der Name eines Benutzers, für den der aktuelle Benutzer IMPERSONATE-Berechtigungen besitzt, oder der Name einer Rolle sein, der der aktuelle Benutzer angehört. Wird diese Klausel nicht angegeben, ist der Nachrichtentyp im Besitz des aktuellen Benutzers.  
  
 VALIDATION  
 Gibt an, wie [!INCLUDE[ssSB](../../includes/sssb-md.md)] den Nachrichtentext für Nachrichten von diesem Typ überprüft. Wird diese Klausel nicht angegeben, ist die Standardeinstellung NONE.  
  
 Keine  
 Gibt an, dass keine Überprüfung erfolgt. Der Nachrichtentext kann beliebige Daten enthalten oder NULL sein.  
  
 EMPTY  
 Gibt an, dass der Nachrichtentext NULL sein muss.  
  
 WELL_FORMED_XML  
 Gibt an, dass der Nachrichtentext wohlgeformte XML-Daten enthalten muss.  
  
 VALID_XML WITH SCHEMA COLLECTION *schema_collection_name*  
 Gibt an, dass der Nachrichtentext XML-Daten enthalten muss, die einem Schema in der angegebenen Schemaauflistung entsprechen. *schema_collection_name* muss der Name einer vorhandenen XML-Schemaauflistung sein.  
  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] überprüft eingehende Nachrichten. Enthält eine Nachricht Text, der nicht dem angegebenen Überprüfungstyp entspricht, verwirft [!INCLUDE[ssSB](../../includes/sssb-md.md)] die ungültige Nachricht und gibt eine Fehlermeldung an den Dienst zurück, der die Nachricht gesendet hat.  
  
 Auf beiden Seiten einer Konversation muss derselbe Name für einen Nachrichtentyp definiert sein. Zur Vereinfachung der Problembehandlung geben beide Seiten einer Konversation in der Regel die gleiche Überprüfung für den Nachrichtentyp an, obwohl [!INCLUDE[ssSB](../../includes/sssb-md.md)] dies nicht voraussetzt.  
  
 Ein Nachrichtentyp kann kein temporäres Objekt sein. Namen von Nachrichtentypen, die mit **#** beginnen, sind zulässig. Hierbei handelt es sich jedoch um dauerhafte Objekte.  
  
## <a name="permissions"></a>Berechtigungen  
 Über die Berechtigung zum Erstellen eines Nachrichtentyps verfügen standardmäßig Mitglieder der festen Datenbankrollen **db_ddladmin** und **db_owner** sowie der festen Serverrolle **sysadmin**.  
  
 Über die REFERENCES-Berechtigung für einen Nachrichtentyp verfügen standardmäßig der Besitzer des Nachrichtentyps, die Mitglieder der festen Datenbankrolle **db_owner** und die Mitglieder der festen Serverrolle **sysadmin**.  
  
 Wenn in der CREATE MESSAGE TYPE-Anweisung eine Schemaauflistung angegeben ist, muss der Benutzer, der die Anweisung ausführt, über die REFERENCES-Berechtigung in der angegebenen Schemaauflistung verfügen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-message-type-containing-well-formed-xml"></a>A. Erstellen eines Nachrichtentyps, der wohlgeformtes XML enthält  
 Im folgenden Beispiel wird ein neuer Nachrichtentyp erstellt, der wohlgeformte XML-Daten enthält.  
  
```  
CREATE MESSAGE TYPE  
  [//Adventure-Works.com/Expenses/SubmitExpense]  
  VALIDATION = WELL_FORMED_XML ;     
```  
  
### <a name="b-creating-a-message-type-containing-typed-xml"></a>B. Erstellen eines Nachrichtentyps, der typisiertes XML enthält  
 Im folgenden Beispiel wird ein Nachrichtentyp für einen Ausgabenbericht erstellt, der in XML verschlüsselt ist. Es wird eine XML-Schemaauflistung erstellt, die das Schema für einen einfachen Ausgabenbericht enthält. Anschließend wird ein neuer Nachrichtentyp erstellt, der Nachrichten mithilfe des Schemas überprüft.  
  
```  
CREATE XML SCHEMA COLLECTION ExpenseReportSchema AS  
N'<?xml version="1.0" encoding="UTF-16" ?>  
  <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
     targetNamespace="http://Adventure-Works.com/schemas/expenseReport"  
     xmlns:expense="http://Adventure-Works.com/schemas/expenseReport"  
     elementFormDefault="qualified"  
   >   
    <xsd:complexType name="expenseReportType">  
       <xsd:sequence>  
         <xsd:element name="EmployeeName" type="xsd:string"/>  
         <xsd:element name="EmployeeID" type="xsd:string"/>  
         <xsd:element name="ItemDetail"  
           type="expense:ItemDetailType" maxOccurs="unbounded"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:complexType name="ItemDetailType">  
      <xsd:sequence>  
        <xsd:element name="Date" type="xsd:date"/>  
        <xsd:element name="CostCenter" type="xsd:string"/>  
        <xsd:element name="Total" type="xsd:decimal"/>  
        <xsd:element name="Currency" type="xsd:string"/>  
        <xsd:element name="Description" type="xsd:string"/>  
      </xsd:sequence>  
    </xsd:complexType>  
  
    <xsd:element name="ExpenseReport" type="expense:expenseReportType"/>  
  
  </xsd:schema>' ;  
  
  CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = VALID_XML WITH SCHEMA COLLECTION ExpenseReportSchema ;  
```  
  
### <a name="c-creating-a-message-type-for-an-empty-message"></a>C. Erstellen eines Nachrichtentyps für eine leere Nachricht  
 Im folgenden Beispiel wird ein neuer Nachrichtentyp mit leerer Codierung erstellt.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = EMPTY ;  
```  
  
### <a name="d-creating-a-message-type-containing-binary-data"></a>D. Erstellen eines Nachrichtentyps, der Binärdaten enthält  
 Im folgenden Beispiel wird ein neuer Nachrichtentyp erstellt, der Binärdaten enthalten soll. Da in der Nachricht keine XML-Daten enthalten sind, wird der Überprüfungstyp vom Nachrichtentyp auf `NONE` festgelegt. Beachten Sie, dass in diesem Fall die Anwendung, die eine Nachricht von diesem Typ empfängt, überprüfen muss, dass die Nachricht Daten enthält und dass die Daten vom erwarteten Typ sind.  
  
```  
CREATE MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/ReceiptImage]  
    VALIDATION = NONE ;  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [ALTER MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
