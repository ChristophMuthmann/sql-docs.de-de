---
title: "Erstellen identischer symmetrischer Schlüssel auf zwei Servern | Microsoft Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4720ac6c86fd531ec4f8b40b14d476dd15511513
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>Erstellen identischer symmetrischer Schlüssel auf zwei Servern
  In diesem Thema wird beschrieben, wie identische symmetrische Schlüssel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mit [!INCLUDE[tsql](../../../includes/tsql-md.md)]auf zwei verschiedenen Servern erstellt werden. Zum Entschlüsseln von verschlüsseltem Text benötigen Sie den Schlüssel, der beim Verschlüsseln verwendet wurde. Wenn eine Datenbank sowohl Verschlüsselungen als auch Entschlüsselungen enthält, ist der Schlüssel in der Datenbank gespeichert, und er ist entsprechend den Berechtigungen sowohl für die Verschlüsselung als auch für die Entschlüsselung verfügbar. Wenn sich Verschlüsselung und Entschlüsselung jedoch in separaten Datenbanken oder auf separaten Servern vorkommt, kann der in einer Datenbank gespeicherte Schlüssel nicht für die zweite Datenbank verwendet werden.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   [So erstellen Sie identische symmetrische Schlüssel auf zwei unterschiedlichen Servern mit Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Beim Erstellen eines symmetrischen Schlüssels muss der symmetrische Schlüssel mithilfe mindestens eines der folgenden Elemente verschlüsselt werden: Zertifikat, Kennwort, symmetrischer Schlüssel, asymmetrischer Schlüssel oder PROVIDER. Der Schlüssel kann mehrere Verschlüsselungen jedes Typs aufweisen. Ein einzelner symmetrischer Schlüssel kann demnach mit mehreren Zertifikaten, Kennwörtern, symmetrischen Schlüsseln und asymmetrischen Schlüsseln gleichzeitig verschlüsselt sein.  
  
-   Wenn ein symmetrischer Schlüssel mit einem Kennwort anstatt mit einem öffentlichen Schlüssel des Datenbank-Hauptschlüssels verschlüsselt ist, wird der TRIPLE_DES-Verschlüsselungsalgorithmus verwendet. Daher werden Schlüssel, die mit einem starken Verschlüsselungsalgorithmus wie z. B. AES erstellt werden, selbst mit einem schwächeren Algorithmus verschlüsselt.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die ALTER ANY SYMMETRIC KEY-Berechtigung in der Datenbank. Falls die AUTHORIZATION-Klausel angegeben ist, ist die IMPERSONATE-Berechtigung für den Datenbankbenutzer oder die ALTER-Berechtigung für die Anwendungsrolle erforderlich. Falls die Verschlüsselung mit einem Zertifikat oder asymmetrischen Schlüssel erfolgt, ist die VIEW DEFINITION-Berechtigung für das Zertifikat oder den asymmetrischen Schlüssel erforderlich. Nur Windows-Anmeldungen, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldungen und Anwendungsrollen können symmetrische Schlüssel besitzen. Gruppen und Rollen können keine symmetrischen Schlüssel besitzen.  
  
##  <a name="TsqlProcedure"></a> Verwenden von Transact-SQL  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>So erstellen Sie identische symmetrische Schlüssel auf zwei verschiedenen Servern  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Erstellen Sie einen Schlüssel, indem Sie die folgenden CREATE MASTER KEY-, CREATE CERTIFICATE- und CREATE SYMMETRIC KEY-Anweisungen ausführen.  
  
    ```  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4.  Stellen Sie eine Verbindung mit einer separaten Serverinstanz her, öffnen Sie ein anderes Abfragefenster, und führen Sie die oben erwähnten SQL-Anweisungen aus, um den gleichen Schlüssel auf dem zweiten Server zu erstellen.  
  
5.  Testen Sie die Schlüssel, indem Sie zunächst die OPEN SYMMETRIC KEY-Anweisung und die SELECT-Anweisung unten auf dem ersten Server ausführen.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  Fügen Sie auf dem zweiten Server das Ergebnis der vorherigen SELECT-Anweisung als Wert für `@blob` in den folgenden Code ein, und führen Sie den folgenden Code aus, um zu überprüfen, ob der verschlüsselte Text mit dem doppelten Schlüssel entschlüsselt werden kann.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  Schließen Sie den symmetrischen Schlüssel auf beiden Servern.  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [CREATE MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ENCRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
  
-   [DECRYPTBYKEY &#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
  
  
