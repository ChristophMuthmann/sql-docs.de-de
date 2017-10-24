---
title: Erstellen von NACHRICHTENTYP (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 04/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f8869a53cf18a58ba58b02e6faf8a42231e971e5
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-message-type-transact-sql"></a>CREATE MESSAGE TYPE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
 Der Name des Nachrichtentyps, der erstellt werden soll. Ein neuer Nachrichtentyp wird in der aktuellen Datenbank erstellt, sein Besitzer ist der in der AUTHORIZATION-Klausel angegebene Prinzipal. Server-, Datenbank- und Schemaname können nicht angegeben werden. Die *Message_type_name* kann bis zu 128 Zeichen sein.  
  
 Autorisierung *Owner_name*  
 Legt den Besitzer des Nachrichtentyps auf den angegebenen Datenbankbenutzer oder die angegebene Datenbankrolle fest. Wenn der aktuelle Benutzer ist **Dbo** oder **sa**, *Owner_name* kann der Name eines beliebigen gültigen Benutzers oder einer Rolle sein. Andernfalls *Owner_name* kann den Namen des aktuellen Benutzers, den Namen eines Benutzers an, die der aktuelle Benutzer IMPERSONATE-Berechtigungen verfügt oder der Name einer Rolle, zu der der aktuelle Benutzer gehört. Wird diese Klausel nicht angegeben, ist der Nachrichtentyp im Besitz des aktuellen Benutzers.  
  
 VALIDATION  
 Gibt an, wie [!INCLUDE[ssSB](../../includes/sssb-md.md)] den Nachrichtentext für Nachrichten von diesem Typ überprüft. Wird diese Klausel nicht angegeben, ist die Standardeinstellung NONE.  
  
 Keine  
 Gibt an, dass keine Überprüfung erfolgt. Der Nachrichtentext kann beliebige Daten enthalten oder NULL sein.  
  
 EMPTY  
 Gibt an, dass der Nachrichtentext NULL sein muss.  
  
 WELL_FORMED_XML  
 Gibt an, dass der Nachrichtentext wohlgeformte XML-Daten enthalten muss.  
  
 VALID_XML WITH SCHEMA COLLECTION *Schema_collection_name*  
 Gibt an, dass der Nachrichtentext XML-Daten enthalten muss, die einem Schema in der angegebenen schemaauflistung entsprechen den *Schema_collection_name* muss der Name einer vorhandenen XML-schemaauflistung sein.  
  
## <a name="remarks"></a>Hinweise  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] überprüft eingehende Nachrichten. Enthält eine Nachricht Text, der nicht dem angegebenen Überprüfungstyp entspricht, verwirft [!INCLUDE[ssSB](../../includes/sssb-md.md)] die ungültige Nachricht und gibt eine Fehlermeldung an den Dienst zurück, der die Nachricht gesendet hat.  
  
 Auf beiden Seiten einer Konversation muss derselbe Name für einen Nachrichtentyp definiert sein. Zur Vereinfachung der Problembehandlung geben beide Seiten einer Konversation in der Regel die gleiche Überprüfung für den Nachrichtentyp an, obwohl [!INCLUDE[ssSB](../../includes/sssb-md.md)] dies nicht voraussetzt.  
  
 Ein Nachrichtentyp kann kein temporäres Objekt sein. Beginnend mit Namen von Nachrichtentypen  **#**  zulässig sind, sind jedoch dauerhafte Objekte.  
  
## <a name="permissions"></a>Berechtigungen  
 Die Berechtigung zum Erstellen eines Nachrichtentyps verfügen standardmäßig Mitglieder der der **Db_ddladmin** oder **Db_owner** festen Datenbankrollen und die **Sysadmin** festen Serverrolle "".  
  
 REFERENCES-Berechtigung für einen Nachrichtentyp standardmäßig verfügen der Besitzer des Nachrichtentyps, der Mitglied der **Db_owner** Datenbankrolle und Mitglieder der festen der **Sysadmin** festen Serverrolle "".  
  
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
  
## <a name="see-also"></a>Siehe auch  
 [ALTER MESSAGE TYPE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

