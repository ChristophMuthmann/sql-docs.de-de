---
title: "Sichern eines Datenbank-Hauptschl&#252;ssels | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenbank-Hauptschlüssel [SQL Server], exportieren"
ms.assetid: 7ad9a0a0-6e4f-4f7b-8801-8c1b9d49c4d8
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# Sichern eines Datenbank-Hauptschl&#252;ssels
  In diesem Thema wird beschrieben, wie der Datenbank-Hauptschlüssel in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[tsql](../../../includes/tsql-md.md)]gesichert wird. Der Datenbank-Hauptschlüssel wird zur Verschlüsselung anderer Schlüssel und Zertifikate in einer Datenbank verwendet. Wenn dieser Schlüssel beschädigt oder gelöscht wird, können die anderen Schlüssel möglicherweise von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nicht entschlüsselt werden, und die damit verschlüsselten Daten gehen verloren. Aus diesem Grund sollten Sie den Datenbank-Hauptschlüssel sichern und diese Sicherung an einem sicheren Ort außerhalb Ihrer Geschäftsräume aufbewahren.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Einschränkungen](#Restrictions)  
  
     [Sicherheit](#Security)  
  
-   [So sichern Sie den Datenbank-Hauptschlüssel mithilfe von Transact-SQL](#Procedure)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Restrictions"></a> Einschränkungen  
  
-   Der Hauptschlüssel muss geöffnet und entschlüsselt sein, bevor er gesichert wird. Wenn er mit dem Diensthauptschlüssel verschlüsselt ist, muss der Hauptschlüssel nicht explizit geöffnet werden. Falls der Hauptschlüssel jedoch nur mit einem Kennwort verschlüsselt ist, muss er explizit geöffnet werden.  
  
-   Es wird empfohlen, dass Sie sofort nach der Erstellung eine Sicherung des Hauptschlüssels anlegen und diese an einem sicheren Ort außerhalb Ihrer Geschäftsräume aufbewahren.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Erfordert die CONTROL-Berechtigung für die Datenbank.  
  
##  <a name="Procedure"></a> Verwenden von SQL Server Management Studio mit Transact-SQL  
  
#### So sichern Sie den Datenbank-Hauptschlüssel  
  
1.  Stellen Sie in [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] eine Verbindung mit der [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Instanz her, die den zu sichernden Datenbank-Hauptschlüssel enthält.  
  
2.  Geben Sie ein Kennwort an, mit dem der Datenbank-Hauptschlüssel auf dem Sicherungsmedium verschlüsselt wird. Dieses Kennwort unterliegt Komplexitätsüberprüfungen.  
  
3.  Verwenden Sie ein Wechselsicherungsmedium, auf dem eine Kopie des gesicherten Schlüssels gespeichert wird.  
  
4.  Ermitteln Sie ein NTFS-Verzeichnis, in dem die Sicherung des Schlüssels erstellt werden soll. In diesem Verzeichnis erstellen Sie die im nächsten Schritt beschriebene Datei. Das Verzeichnis sollte durch stark einschränkende Zugriffssteuerungslisten (Access Control Lists, ACLs) geschützt sein.  
  
5.  Stellen Sie im Objekt-Explorer ** **eine Verbindung mit einer [!INCLUDE[ssDE](../../../includes/ssde-md.md)]-Instanz her.  
  
6.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
7.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- Creates a backup of the "AdventureWorks2012" master key. Because this master key is not encrypted by the service master key, a password must be specified when it is opened.  
    USE AdventureWorks2012;   
    GO  
    OPEN MASTER KEY DECRYPTION BY PASSWORD = 'sfj5300osdVdgwdfkli7';   
  
    BACKUP MASTER KEY TO FILE = 'c:\temp\exportedmasterkey'   
        ENCRYPTION BY PASSWORD = 'sd092735kjn$&adsg';   
    GO  
    ```  
  
    > [!NOTE]  
    >  Der Dateipfad zum Schlüssel und das Kennwort (sofern es vorhanden ist) des Schlüssels unterscheiden sich von den obigen Informationen. Stellen Sie sicher, dass beide für den Server und die Schlüsseleinrichtung spezifisch sind.  
  
8.  Kopieren Sie die Datei auf das Sicherungsmedium, und überprüfen Sie die Kopie.  
  
9. Verwahren Sie die Sicherung an einem sicheren Ort außerhalb der Geschäftsräume.  
  
 Weitere Informationen finden Sie unter [OPEN MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/open-master-key-transact-sql.md) und [BACKUP MASTER KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/backup-master-key-transact-sql.md).  
  
  