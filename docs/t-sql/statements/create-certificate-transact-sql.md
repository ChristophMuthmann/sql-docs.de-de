---
title: Erstellen von CERTIFICATE (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CERTIFICATE
- CREATE_CERTIFICATE_TSQL
- sql13.swb.createcertificate.f1
- CERTIFICATE_TSQL
- CREATE CERTIFICATE
- sql13.swb.certificateproperties.f1
dev_langs:
- TSQL
helpviewer_keywords:
- encryption [SQL Server], certificates
- certificates [SQL Server], adding
- certificates [SQL Server]
- adding certificates
- cryptography [SQL Server], certificates
- CREATE CERTIFICATE statement
ms.assetid: a4274b2b-4cb0-446a-a956-1c8e6587515d
caps.latest.revision: 74
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8753e820278eb04fff6f12e405d766fff5292e58
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-certificate-transact-sql"></a>CREATE CERTIFICATE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Fügt einer Datenbank in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ein Zertifikat hinzu.  
  
 Diese Funktion ist inkompatibel mit Datenbankexport über Data-Tier Application Framework (DACFx). Sie müssen alle Zertifikate vor dem Export löschen.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
CREATE CERTIFICATE certificate_name [ AUTHORIZATION user_name ]   
    { FROM <existing_keys> | <generate_new_keys> }  
    [ ACTIVE FOR BEGIN_DIALOG =  { ON | OFF } ]  
  
<existing_keys> ::=   
    ASSEMBLY assembly_name  
    | {   
        [ EXECUTABLE ] FILE = 'path_to_file'  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]   
      }  
    | {   
        BINARY = asn_encoded_certificate  
        [ WITH PRIVATE KEY ( <private_key_options> ) ]  
      }  
<generate_new_keys> ::=   
    [ ENCRYPTION BY PASSWORD = 'password' ]   
    WITH SUBJECT = 'certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<private_key_options> ::=  
      {   
        FILE = 'path_to_private_key'  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
    |  
      {   
        BINARY = private_key_bits  
         [ , DECRYPTION BY PASSWORD = 'password' ]  
         [ , ENCRYPTION BY PASSWORD = 'password' ]    
      }  
  
<date_options> ::=  
    START_DATE = 'datetime' | EXPIRY_DATE = 'datetime'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE CERTIFICATE certificate_name   
    { <generate_new_keys> | FROM <existing_keys> }  
    [ ; ]  
  
<generate_new_keys> ::=   
    WITH SUBJECT ='certificate_subject_name'   
    [ , <date_options> [ ,...n ] ]   
  
<existing_keys> ::=   
    {   
      FILE ='path_to_file'  
      WITH PRIVATE KEY   
         (   
           FILE ='path_to_private_key'  
           , DECRYPTION BY PASSWORD ='password'   
         )  
    }  
  
<date_options> ::=  
    START_DATE ='datetime' | EXPIRY_DATE ='datetime'  
```  
  
## <a name="arguments"></a>Argumente  
 *Name*  
 Ist der Name für das Zertifikat in der Datenbank.  
  
 Autorisierung *User_name*  
 Ist der Name des Benutzers, der Besitzer dieses Zertifikats ist.  
  
 ASSEMBLY *Assembly_name*  
 Gibt eine signierte Assembly an, die bereits in die Datenbank geladen wurde.  
  
 [AUSFÜHRBARE DATEI] Datei ='*Dateipfad*"  
 Gibt den vollständigen Pfad einschließlich des Dateinamens zur DER-codierten Datei an, die das Zertifikat enthält. Falls die EXECUTABLE-Option verwendet wird, handelt es sich bei der Datei um eine DLL-Datei, die mit dem Zertifikat signiert wurde. *Dateipfad* kann ein lokaler Pfad oder einen UNC-Pfad zu einem Netzwerkspeicherort sein. Die Datei wird im Sicherheitskontext des zugegriffen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto. Dieses Konto muss über die erforderlichen Dateisystemberechtigungen verfügen.  
  
 WITH PRIVATE KEY  
 Gibt an, dass der private Schlüssel des Zertifikats in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] geladen wird. Diese Klausel ist nur gültig, wenn das Zertifikat aus einer Datei erstellt wird. Um den privaten Schlüssel einer Assembly zu laden, verwenden [ALTER CERTIFICATE](../../t-sql/statements/alter-certificate-transact-sql.md).  
  
 Datei ='*Path_to_private_key*"  
 Gibt den vollständigen Pfad einschließlich des Dateinamens für den privaten Schlüssel an. *Path_to_private_key* kann ein lokaler Pfad oder einen UNC-Pfad zu einem Netzwerkspeicherort sein. Die Datei wird im Sicherheitskontext des zugegriffen der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Dienstkonto. Dieses Konto muss über die erforderlichen Dateisystemberechtigungen verfügen.  
  
> [!NOTE]  
>  Diese Option ist in einer enthaltenen Datenbank nicht verfügbar.  
  
 asn_encoded_certificate  
 Mit ASN verschlüsselte Zertifikatbits, die als binäre Konstante angegeben sind.  
  
 BINÄRE =*Private_key_bits*  
 **Gilt für**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] bis [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Private Schlüsselbits, die als binäre Konstante angegeben sind. Diese Bits können in verschlüsselter Form vorhanden sein. Bei Verschlüsselung muss der Benutzer ein Entschlüsselungskennwort bereitstellen. Kennwortrichtlinienüberprüfungen werden für dieses Kennwort nicht ausgeführt. Die privaten Schlüsselbits müssen in einem PVK-Dateiformat vorliegen.  
  
 DECRYPTION BY PASSWORD = "*Key_password*"  
 Gibt das Kennwort an, das zum Entschlüsseln eines privaten Schlüssels erforderlich ist, der aus einer Datei abgerufen wird. Diese Klausel ist optional, wenn der private Schlüssel nicht durch ein Kennwort geschützt ist. Das Speichern eines privaten Schlüssels in einer Datei ohne Kennwortschutz wird nicht empfohlen. Wenn ein Kennwort erforderlich ist, jedoch kein Kennwort angegeben ist, schlägt die Anweisung fehl.  
  
 ENCRYPTION BY PASSWORD = "*Kennwort*"  
 Gibt an, das zum Verschlüsseln des privaten Schlüssels verwendete Kennwort. Verwenden Sie diese Option nur, wenn Sie das Zertifikat mit einem Kennwort verschlüsseln möchten. Wenn diese Klausel weggelassen wird, wird der private Schlüssel mit dem Datenbank-Hauptschlüssel verschlüsselt. *Kennwort* erfüllt die Anforderungen der Windows-Kennwortrichtlinien des Computers, der die Instanz ausgeführt wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Weitere Informationen finden Sie unter [Password Policy](../../relational-databases/security/password-policy.md).  
  
 SUBJECT = "*Zertifikatantragstellername ein*"  
 Der Begriff *Betreff* bezieht sich auf ein Feld in den Metadaten des Zertifikats im x. 509-Standard definiert. Das Thema sollte nicht mehr als 64 Zeichen lang sein und wird dieser Grenzwert für erzwungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Linux. Für [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unter Windows der Antragsteller kann bis zu 128 Zeichen lang sein. Themen, die mehr 128 Zeichen als werden abgeschnitten, wenn sie die im Katalog gespeichert sind, aber binary large Object (BLOB), die das Zertifikat enthält, der vollständige Name des Antragstellers behält.  
  
 Start_date = "*" DateTime "*"  
 Das Datum, an dem das Zertifikat gültig wird. Wenn nicht angegeben, wird die START_DATE gleich dem aktuellen Datum festgelegt. START_DATE ist in UTC-Zeit und kann in jedem Format angegeben werden, das in ein Datum und eine Uhrzeit konvertiert werden kann.  
  
 EXPIRY_DATE = "*" DateTime "*"  
 Das Datum, an dem das Zertifikat abläuft. Wenn nicht angegeben, wird EXPIRY_DATE auf ein Datum ein Jahr nach START_DATE festgelegt. EXPIRY_DATE ist in UTC-Zeit und kann in jedem Format angegeben werden, das in ein Datum und eine Uhrzeit konvertiert werden kann. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Service Broker prüft das Ablaufdatum. Ablauf wird jedoch nicht erzwungen, wenn das Zertifikat für die Verschlüsselung verwendet wird.  
  
 ACTIVE FOR BEGIN_DIALOG = { **ON** | {OFF}  
 Stellt das Zertifikat für den Initiator einer [!INCLUDE[ssSB](../../includes/sssb-md.md)]-Dialogkonversation zur Verfügung. Der Standardwert ist ON.  
  
## <a name="remarks"></a>Hinweise  
 Ein Zertifikat ist ein sicherungsfähiges Element auf Datenbankebene, das dem X.509-Standard entspricht und X.509 V1-Felder unterstützt. CREATE CERTIFICATE kann ein Zertifikat aus einer Datei oder Assembly laden. Mit dieser Anweisung kann auch ein Schlüsselpaar generiert und ein selbstsigniertes Zertifikat erstellt werden.  
  
 Der Private Schlüssel muss \<= 2500 Bytes in einem verschlüsselten Format. Vom generierten privaten Schlüssel [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind 1024 Bits lang über [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] und 2048 Bits lang beginnen mit [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]. Private Schlüssel, die aus einer externen Quelle importiert werden, haben eine minimale Länge von 384 Bits und eine maximale Länge von 4.096 Bits. Die Länge eines importierten privaten Schlüssels muss ein ganzzahliges Produkt von 64 Bits sein. Die für TDE verwendeten Zertifikate sind auf die private Schlüsselgröße von 3456 Bits beschränkt.  
  
 Die gesamte Seriennummer des Zertifikats gespeichert ist, aber nur die ersten 16 Bytes, die in der sys.certificates-Katalogsicht angezeigt werden.  
  
 Das gesamte Feld Aussteller desselben Zertifikats gespeichert ist, aber nur die ersten 884 Bytes in der sys.certificates-Katalogsicht.  
  
 Der private Schlüssel muss dem öffentlichen Schlüssel gemäß entsprechen *Name*.  
  
 Beim Erstellen eines Zertifikats aus einem Container ist das Laden des privaten Schlüssels optional. Wenn von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] jedoch ein selbstsigniertes Zertifikat generiert wird, wird der private Schlüssel immer erstellt. Standardmäßig ist der private Schlüssel mit dem Datenbank-Hauptschlüssel verschlüsselt. Wenn die Datenbank-Hauptschlüssel ist nicht vorhanden, und kein Kennwort angegeben ist, schlägt die Anweisung fehl.  
  
 Die ENCRYPTION BY PASSWORD-Option ist nicht erforderlich, wenn der private Schlüssel mit dem Datenbank-Hauptschlüssel verschlüsselt ist. Verwenden Sie diese Option nur, wenn der private Schlüssel mit einem Kennwort verschlüsselt ist. Falls kein Kennwort angegeben ist, wird der private Schlüssel des Zertifikats mit dem Datenbank-Hauptschlüssel verschlüsselt. Wenn der Hauptschlüssel der Datenbank nicht geöffnet werden kann, verursacht diese Klausel ausgelassen einen Fehler.  
  
 Sie müssen kein Entschlüsselungskennwort angeben, wenn der private Schlüssel mit dem Datenbank-Hauptschlüssel verschlüsselt ist.  
  
> [!NOTE]  
>  Die Ablaufdaten von Zertifikaten werden von integrierten Funktionen für die Verschlüsselung und Signierung nicht überprüft. Benutzer dieser Funktionen müssen entscheiden, wann die Ablaufdaten der Zertifikate überprüft werden sollen.  
  
 Eine binäre Beschreibung eines Zertifikats kann erstellt werden, mithilfe der [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md) und [CERTPRIVATEKEY &#40; Transact-SQL &#41; ](../../t-sql/functions/certprivatekey-transact-sql.md) Funktionen. Ein Beispiel, verwendet **CERTPRIVATEKEY** und **CERTENCODED** zum Kopieren eines Zertifikats in eine andere Datenbank finden Sie unter Beispiel B im Thema [CERTENCODED &#40; Transact-SQL &#41; ](../../t-sql/functions/certencoded-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die CREATE CERTIFICATE-Berechtigung für die Datenbank. Nur Windows-Anmeldungen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Anmeldenamen und Anwendungsrollen können Zertifikate besitzen. Gruppen und Rollen können keine Zertifikate besitzen.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-creating-a-self-signed-certificate"></a>A. Erstellen eines selbstsignierten Zertifikats  
 Im folgenden Beispiel wird ein Zertifikat namens `Shipping04` erstellt. Der private Schlüssel dieses Zertifikats wird mit einem Kennwort geschützt.  
  
```  
CREATE CERTIFICATE Shipping04   
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
   WITH SUBJECT = 'Sammamish Shipping Records',   
   EXPIRY_DATE = '20201031';  
GO  
```  
  
### <a name="b-creating-a-certificate-from-a-file"></a>B. Erstellen eines Zertifikats aus einer Datei  
 Im folgenden Beispiel wird ein Zertifikat in der Datenbank erstellt, wobei das Schlüsselpaar aus Dateien geladen wird.  
  
```  
CREATE CERTIFICATE Shipping11   
    FROM FILE = 'c:\Shipping\Certs\Shipping11.cer'   
    WITH PRIVATE KEY (FILE = 'c:\Shipping\Certs\Shipping11.pvk',   
    DECRYPTION BY PASSWORD = 'sldkflk34et6gs%53#v00');  
GO   
```  
  
### <a name="c-creating-a-certificate-from-a-signed-executable-file"></a>C. Erstellen eines Zertifikats aus einer signierten ausführbaren Datei  
  
```  
CREATE CERTIFICATE Shipping19   
    FROM EXECUTABLE FILE = 'c:\Shipping\Certs\Shipping19.dll';  
GO  
```  
  
 Alternativ können Sie eine Assembly aus der `dll`-Datei erstellen und anschließend ein Zertifikat aus der Assembly erstellen.  
  
```  
CREATE ASSEMBLY Shipping19   
    FROM ' c:\Shipping\Certs\Shipping19.dll'   
    WITH PERMISSION_SET = SAFE;  
GO  
CREATE CERTIFICATE Shipping19 FROM ASSEMBLY Shipping19;  
GO  
```  
  
### <a name="d-creating-a-self-signed-certificate"></a>D. Erstellen eines selbstsignierten Zertifikats  
 Das folgende Beispiel erstellt ein Zertifikat namens `Shipping04` ohne ein Verschlüsselungskennwort. Dieses Beispiel kann verwendet werden, mit [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] und [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
```  
CREATE CERTIFICATE Shipping04   
   WITH SUBJECT = 'Sammamish Shipping Records';  
GO  
```  
  
  
## <a name="see-also"></a>Siehe auch  
 [ALTER CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Verschlüsselungshierarchie](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [CERTENCODED &#40; Transact-SQL &#41;](../../t-sql/functions/certencoded-transact-sql.md)   
 [CERTPRIVATEKEY &#40; Transact-SQL &#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
  
  



