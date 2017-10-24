---
title: "Signatur hinzufügen (Transact-SQL) | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ADD SIGNATURE
- ADD_SIGNATURE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ADD SIGNATURE statement
- adding digital signatures
- signatures [SQL Server]
- digital signatures [SQL Server]
ms.assetid: 64d8b682-6ec1-4e5b-8aee-3ba11e72d21f
caps.latest.revision: 50
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d171b17749cbe5333a11405eb48ac4b9293151d6
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="add-signature-transact-sql"></a>ADD SIGNATURE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Fügt einer gespeicherten Prozedur, einer Funktion, einer Assembly oder einem Trigger eine digitale Signatur hinzu. Fügt einer gespeicherten Prozedur, einer Funktion, einer Assembly oder einem Trigger außerdem eine Gegensignatur hinzu.  
  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
ADD [ COUNTER ] SIGNATURE TO module_class::module_name   
    BY <crypto_list> [ ,...n ]  
  
<crypto_list> ::=  
    CERTIFICATE cert_name  
    | CERTIFICATE cert_name [ WITH PASSWORD = 'password' ]  
    | CERTIFICATE cert_name WITH SIGNATURE = signed_blob   
    | ASYMMETRIC KEY Asym_Key_Name  
    | ASYMMETRIC KEY Asym_Key_Name [ WITH PASSWORD = 'password'.]  
    | ASYMMETRIC KEY Asym_Key_Name WITH SIGNATURE = signed_blob  
```  
  
## <a name="arguments"></a>Argumente  
 *module_class*  
 Die Klasse des Moduls, dem die Signatur hinzugefügt wird. Der Standard für Module, die Schemas als Bereiche besitzen, ist OBJECT.  
  
 *Modulname*  
 Der Name einer gespeicherten Prozedur, einer Funktion, einer Assembly oder eines Triggers, die bzw. der signiert oder gegensigniert werden soll.  
  
 Zertifikat *Cert_name*  
 Der Name eines Zertifikats, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert oder gegensigniert werden soll.  
  
 MIT dem Kennwort = "*Kennwort*"  
 Das Kennwort, das zum Entschlüsseln des privaten Schlüssels des Zertifikats oder asymmetrischen Schlüssels erforderlich ist. Diese Klausel ist nur erforderlich, wenn der private Schlüssel nicht durch den Hauptschlüssel für die Datenbank geschützt ist.  
  
 Signatur =*Signed_blob*  
 Gibt das signierte BLOB-Element des Moduls an. Diese Klausel ist hilfreich, wenn Sie ein Modul ohne den privaten Schlüssel versenden möchten. Bei Verwendung dieser Klausel sind nur das Modul, die Signatur und der öffentliche Schlüssel erforderlich, um das signierte BLOB-Element für eine Datenbank zu signieren. *Signed_blob* Blob selbst im Hexadezimalformat angegeben ist.  
  
 ASYMMETRISCHE Schlüssel *Asym_Key_Name*  
 Der Name eines asymmetrischen Schlüssels, mit dem die gespeicherte Prozedur, die Funktion, die Assembly oder der Trigger signiert oder gegensigniert werden soll.  
  
## <a name="remarks"></a>Hinweise  
 Das Modul, das signiert oder gegensigniert wird, und das Zertifikat oder der asymmetrische Schlüssel, das bzw. der zum Signieren verwendet wird, müssen bereits vorhanden sein. Jedes Zeichen im Modul ist in der Signaturberechnung enthalten. Hierzu gehören auch führende Wagenrückläufe und Zeilenvorschübe.  
  
 Ein Modul kann mit einer beliebigen Anzahl von Zertifikaten und asymmetrischen Schlüsseln signiert oder gegensigniert werden.  
  
 Die Signatur eines Moduls wird bei Änderung des Moduls gelöscht.  
  
 Wenn ein Modul eine EXECUTE AS-Klausel enthält, ist auch die Sicherheits-ID (SID) des Prinzipals im Signierungsvorgang enthalten.  
  
> [!CAUTION]  
>  Module dürfen nur beim Erteilen von Berechtigungen signiert werden, nie beim Verweigern oder Aufheben von Berechtigungen.  
  
 Inline-Tabellenwertfunktionen können nicht signiert werden.  
  
 Informationen zu Signaturen werden in der sys.crypt_properties-Katalogsicht angezeigt.  
  
> [!WARNING]  
>  Wenn Sie eine Prozedur zur Signatur neu erstellen, müssen alle Anweisungen im ursprünglichen Batch mit dem Neuerstellungsbatch übereinstimmen. Wenn ein Teil des Batches anders ist, selbst wenn es sich nur um die Leerzeichen oder Kommentare handelt, unterscheidet sich auch die daraus resultierende Signatur.  
  
## <a name="countersignatures"></a>Gegensignaturen  
 Beim Ausführen eines signierten Moduls die Signaturen werden vorübergehend hinzugefügt werden mit dem SQL-Token, aber die Signaturen verloren, wenn das Modul ein weiteres Modul ausführt oder wenn die Ausführung beendet. Eine Gegensignatur ist eine besondere Form der Signatur. Eine Gegensignatur gewährt selbst keine Berechtigungen, sie lässt jedoch zu, dass Signaturen, die vom selben Zertifikat oder asymmetrischen Schlüssel erstellt wurden, über die Dauer des Aufrufs des gegensignierten Objekts beibehalten werden.  
  
 Beispiel: Die Benutzerin Alice ruft die Prozedur ProcSelectT1ForAlice auf, die wiederum die Prozedur procSelectT1 aufruft, von der eine Auswahl in Tabelle T1 getroffen wird. Alice verfügt über die EXECUTE-Berechtigung für ProcSelectT1ForAlice und procSelectT1, aber sie verfügt nicht über die SELECT-Berechtigung für T1. Außerdem weist die gesamte Kette keine Besitzverkettung auf. Alice kann weder direkt noch über ProcSelectT1ForAlice und procSelectT1 auf die Tabelle T1 zugreifen. Da Alice soll für den Zugriff immer ProcSelectT1ForAlice verwenden soll, möchten wir nicht gewähren der Berechtigung zur Ausführung von proselectt1. Welche Vorgehensweise empfiehlt sich?  
  
-   Wenn procSelectT1 signiert wird, sodass procSelectT1 auf T1 zugreifen kann, ist Alice in der Lage, procSelectT1 direkt aufzurufen, ohne ProcSelectT1ForAlice aufzurufen.  
  
-   Die EXECUTE-Berechtigung für procSelectT1 könnte Alice verweigert werden, allerdings wäre sie dann auch nicht in der Lage, procSelectT1 über ProcSelectT1ForAlice aufzurufen.  
  
-   Das Signieren von ProcSelectT1ForAlice funktioniert alleine nicht, weil die Signatur im Aufruf von procSelectT1 verloren gehen würde.  
  
Doch durch gegensigniert procSelectT1 mit demselben Zertifikat zum Signieren von ProcSelectT1ForAlice, verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] hält die Signatur gesamten Aufrufkette und ermöglicht den Zugriff auf T1. Wenn Alice versucht, procSelectT1 direkt aufzurufen, ist kein Zugriff auf T1 möglich, weil durch die Gegensignatur keine Rechte gewährt werden. In Beispiel C unten wird [!INCLUDE[tsql](../../includes/tsql-md.md)] für dieses Beispiel veranschaulicht.  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die ALTER-Berechtigung für das Objekt und die CONTROL-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel. Falls ein zugeordneter privater Schlüssel mit einem Kennwort geschützt ist, muss der Benutzer zudem das Kennwort kennen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-signing-a-stored-procedure-by-using-a-certificate"></a>A. Signieren einer gespeicherten Prozedur mithilfe eines Zertifikats  
 Im folgenden Beispiel wird die gespeicherte Prozedur `HumanResources.uspUpdateEmployeeLogin` mit dem Zertifikat `HumanResourcesDP` signiert.  
  
```  
USE AdventureWorks2012;  
ADD SIGNATURE TO HumanResources.uspUpdateEmployeeLogin   
    BY CERTIFICATE HumanResourcesDP;  
GO  
```  
  
### <a name="b-signing-a-stored-procedure-by-using-a-signed-blob"></a>B. Signieren einer gespeicherten Prozedur mithilfe eines signierten BLOB-Elements  
 Im folgenden Beispiel werden eine neue Datenbank und ein Zertifikat erstellt, die im Beispiel verwendet werden sollen. Im Beispiel wird eine einfache gespeicherte Prozedur erstellt und signiert sowie die Signatur-BLOB aus `sys.crypt_properties` abgerufen. Die Signatur wird dann gelöscht und erneut hinzugefügt. Im Beispiel wird die Prozedur mithilfe der WITH SIGNATURE-Syntax signiert.  
  
```  
CREATE DATABASE TestSignature ;  
GO  
USE TestSignature ;  
GO  
-- Create a CERTIFICATE to sign the procedure.  
CREATE CERTIFICATE cert_signature_demo   
    ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
    WITH SUBJECT = 'ADD SIGNATURE demo';  
GO  
-- Create a simple procedure.  
CREATE PROC [sp_signature_demo]  
AS  
    PRINT 'This is the content of the procedure.' ;  
GO  
-- Sign the procedure.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]   
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y' ;  
GO  
-- Get the signature binary BLOB for the sp_signature_demo procedure.  
SELECT cp.crypt_property  
    FROM sys.crypt_properties AS cp  
    JOIN sys.certificates AS cer  
        ON cp.thumbprint = cer.thumbprint  
    WHERE cer.name = 'cert_signature_demo' ;  
GO  
```  
  
 Die von dieser Anweisung zurückgegebene `crypt_property`-Signatur ist bei jeder erstellten Prozedur anders. Notieren Sie sich das Ergebnis, um es später in diesem Beispiel zu verwenden. Für dieses Beispiel lautet das Ergebnis wie folgt: `0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373`.  
  
```  
-- Drop the signature so that it can be signed again.  
DROP SIGNATURE FROM [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo];  
GO  
-- Add the signature. Use the signature BLOB obtained earlier.  
ADD SIGNATURE TO [sp_signature_demo]   
    BY CERTIFICATE [cert_signature_demo]  
    WITH SIGNATURE = 0x831F5530C86CC8ED606E5BC2720DA835351E46219A6D5DE9CE546297B88AEF3B6A7051891AF3EE7A68EAB37CD8380988B4C3F7469C8EABDD9579A2A5C507A4482905C2F24024FFB2F9BD7A953DD5E98470C4AA90CE83237739BB5FAE7BAC796E7710BDE291B03C43582F6F2D3B381F2102EEF8407731E01A51E24D808D54B373 ;  
GO  
```  
  
### <a name="c-accessing-a-procedure-using-a-countersignature"></a>C. Zugreifen auf eine Prozedur mithilfe einer Gegensignatur  
 Im folgenden Beispiel wird gezeigt, wie durch das Gegensignieren der Zugriff auf ein Objekt gesteuert wird.  
  
```  
-- Create tesT1 database  
CREATE DATABASE testDB;  
GO  
USE testDB;  
GO  
-- Create table T1  
CREATE TABLE T1 (c varchar(11));  
INSERT INTO T1 VALUES ('This is T1.');  
  
-- Create a TestUser user to own table T1  
CREATE USER TestUser WITHOUT LOGIN;  
ALTER AUTHORIZATION ON T1 TO TestUser;  
  
-- Create a certificate for signing  
CREATE CERTIFICATE csSelectT  
  ENCRYPTION BY PASSWORD = 'SimplePwd01'  
  WITH SUBJECT = 'Certificate used to grant SELECT on T1';  
CREATE USER ucsSelectT1 FROM CERTIFICATE csSelectT;  
GRANT SELECT ON T1 TO ucsSelectT1;  
  
-- Create a principal with low privileges  
CREATE LOGIN Alice WITH PASSWORD = 'SimplePwd01';  
CREATE USER Alice;  
  
-- Verify Alice cannoT1 access T1;  
EXECUTE AS LOGIN = 'Alice';  
    SELECT * FROM T1;  
REVERT;  
  
-- Create a procedure that directly accesses T1  
CREATE PROCEDURE procSelectT1 AS  
BEGIN  
    PRINT 'Now selecting from T1...';  
    SELECT * FROM T1;  
END;  
GO  
GRANT EXECUTE ON procSelectT1 to public;  
  
-- Create special procedure for accessing T1  
CREATE PROCEDURE  procSelectT1ForAlice AS  
BEGIN  
   IF USER_ID() <> USER_ID('Alice')  
    BEGIN  
        PRINT 'Only Alice can use this.';  
        RETURN  
    END  
   EXEC procSelectT1;  
END;  
GO;  
GRANT EXECUTE ON procSelectT1ForAlice TO PUBLIC;  
  
-- Verify procedure works for a sysadmin user  
EXEC procSelectT1ForAlice;  
  
-- Alice still can't use the procedure yet  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
REVERT;  
  
-- Sign procedure to grant it SELECT permission  
ADD SIGNATURE TO procSelectT1ForAlice BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Counter sign proc_select_t, to make this work  
ADD COUNTER SIGNATURE TO procSelectT1 BY CERTIFICATE csSelectT   
WITH PASSWORD = 'SimplePwd01';  
  
-- Now the proc works.   
-- Note that calling procSelectT1 directly still doesn't work  
EXECUTE AS LOGIN = 'Alice';  
    EXEC procSelectT1ForAlice;  
    EXEC procSelectT1;  
REVERT;  
  
-- Cleanup  
USE master;  
GO  
DROP DATABASE testDB;  
DROP LOGIN Alice;  
  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sys. crypt_properties &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)   
 [Löschen Sie die Signatur &#40; Transact-SQL &#41;](../../t-sql/statements/drop-signature-transact-sql.md)  
  
  

