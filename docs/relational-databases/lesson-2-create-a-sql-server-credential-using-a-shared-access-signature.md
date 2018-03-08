---
title: 'Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS) | Microsoft-Dokumentation'
ms.custom: 
ms.date: 02/25/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 29e57ebd-828f-4dff-b473-c10ab0b1c597
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9de61b250b8605e5f47a58ff7bb77e10c54ab123
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="lesson-2-create-a-sql-server-credential-using-a-shared-access-signature"></a>Lektion 2: Erstellen von SQL Server-Anmeldeinformationen mit einer Shared Access Signature (SAS)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
In dieser Lektion erstellen Sie Anmeldeinformationen zum Speichern der Sicherheitsinformationen, die von SQL Server verwendet wird, um in einen Azure-Container zu schreiben und aus diesem zu lesen, den Sie in [Lektion 1: Erstellen einer Richtlinie und einer Shared Access Signature (SAS) in einem Azure-Container](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)erstellt haben.  
  
SQL Server-Anmeldeinformationen sind ein Objekt zum Speichern von Authentifizierungsinformationen, die für die Verbindung mit einer Ressource außerhalb von SQL Server erforderlich sind. In den Anmeldeinformationen werden der URI-Pfad des Speichercontainers und die Shared Access Signature für diesen Container gespeichert.  
  
> [!NOTE]  
> Wenn Sie eine SQL Server 2012 SP1 CU2 oder höhere Datenbank oder eine SQL Server 2014-Datenbank in diesem Azure-Container sichern möchten, können Sie die hier dokumentierte [veraltete Syntax](https://technet.microsoft.com/en-US/library/dn435916(v=sql.120).aspx) verwenden, um SQL Server-Anmeldeinformationen basierend auf Ihrem Schlüssel für das Speicherkonto zu erstellen.  
  
## <a name="create-sql-server-credential"></a>Erstellen von SQL Server-Anmeldeinformationen  
Führen Sie die folgenden Schritte aus, um SQL Server-Anmeldeinformationen zu erstellen:  
  
1.  Stellen Sie eine Verbindung mit SQL Server Management Studio her.  
  
2.  Öffnen Sie ein neues Abfragefenster und stellen Sie eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls in Ihrer lokalen Umgebung.  
  
3.  Fügen Sie in das neue Abfragefenster die CREATE CREDENTIAL-Anweisung mit der SAS aus Lektion 1 ein, und führen Sie dieses Skript aus.  
  
    Das Skript wird wie der folgende Code aussehen.  
  
    ```Transact-SQL  
  
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] – this name must match the container path, start with https and must not contain a forward slash.  
       WITH IDENTITY='SHARED ACCESS SIGNATURE' -- this is a mandatory string and do not change it.   
       , SECRET = 'sharedaccesssignature' –- this is the shared access signature key that you obtained in Lesson 1.   
    GO  
  
    ```  
  
4.  Um alle verfügbaren Anmeldeinformationen anzuzeigen, können Sie die folgende Anweisung in einem Abfragefenster ausführen, das mit Ihrer Instanz verbunden ist:  
  
    ```Transact-SQL  
    SELECT * from sys.credentials  
    ```  
  
5.  Öffnen Sie ein neues Abfragefenster und stellen Sie eine Verbindung mit der SQL Server 2016-Instanz des Datenbankmoduls auf Ihrem virtuellen Azure-Computer her.  
  
6.  Fügen Sie in das neue Abfragefenster die CREATE CREDENTIAL-Anweisung mit der SAS aus Lektion 1 ein, und führen Sie dieses Skript aus.  
  
7.  Wiederholen Sie die Schritte 5 und 6 für alle zusätzlichen SQL Server 2016-Instanzen, die auf den Azure-Container zugreifen sollen.  
  
**Nächste Lektion:**  
  
[Lektion 3: Datenbanksicherung über URLs](../relational-databases/lesson-3-database-backup-to-url.md)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Anmeldeinformationen &#40;Datenbankmodul&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials &#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
  

