---
title: RESTORE DATABASE (Parallel Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/17/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: d915bfc1-e392-4a3a-9d94-08682cf3c864
caps.latest.revision: 8
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 001813cf0e7d00e089046d8580108eb10ef4cba0
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="restore-database-parallel-data-warehouse"></a>Wiederherstellen der Datenbank (Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Wiederhergestellt eine [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Benutzerdatenbank von einer datenbanksicherung auf einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance. Wiederherstellung der Datenbank aus einer Sicherung, die zuvor von erstellt die [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] [BACKUP DATABASE &#40; Parallel Datawarehouse &#41; ](../../t-sql/statements/backup-database-parallel-data-warehouse.md) Befehl. Das Sichern und Wiederherstellen in einen Notfallwiederherstellungsplan erstellen oder Datenbanken aus einer Anwendung auf einen anderen verschoben.  
  
> [!NOTE]  
>  Wiederherstellen der Master enthält Anmeldeinformationen Appliance wiederherstellen. Verwenden Sie zum Wiederherstellen der Master der [Wiederherstellen der master-Datenbank &#40; Transact-SQL &#41; ](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md) auf der Seite der **Configuration Manager** Tool. Ein Administrator mit Zugriff auf den Knoten "Zugriffssteuerung" kann diesen Vorgang ausführen.  
  
 Weitere Informationen zu [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] datenbanksicherungen, finden Sie unter "Sichern und Wiederherstellen" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Restore the master database  
-- Use the Configuration Manager tool.  
  
Restore a full user database backup.  
RESTORE DATABASE database_name   
    FROM DISK = '\\UNC_path\full_backup_directory'  
[;]  
  
Restore a full user database backup and then a differential backup.  
RESTORE DATABASE database_name  
    FROM DISK = '\\UNC_path\differential_backup_directory'   
    WITH [ ( ] BASE = '\\UNC_path\full_backup_directory' [ ) ]   
[;]  
  
Restore header information for a full or differential user database backup.  
RESTORE HEADERONLY   
    FROM DISK = '\\UNC_path\backup_directory'  
[;]  
```  
  
## <a name="arguments"></a>Argumente  
 RESTORE DATABASE *Database_name*  
 Gibt an, dass eine Datenbank mit dem Namen eine Benutzerdatenbank wiederherstellen *Database_name*. Die wiederhergestellte Datenbank kann einen anderen Namen als die Quelldatenbank verfügen, die gesichert wurde. *Database_name* kann nicht als eine Datenbank auf dem Gerät Ziel bereits vorhanden. Weitere Informationen zu den Datenbanknamen zulässig "Benennungsregeln für Objekt" finden Sie unter der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Eine Benutzerdatenbank wiederherstellen eine vollständigen datenbanksicherung wiederhergestellt und anschließend optional eine differenzielle Sicherung in der Einheit wiederhergestellt. Eine Wiederherstellung einer Benutzerdatenbank enthält wiederherstellen, Datenbankbenutzer und Datenbankrollen.  
  
 FROM DISK = '\\\\*UNC_path*\\*Backup_directory*"  
 Der Netzwerkpfad und das Verzeichnis, aus dem [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] werden die Sicherungsdateien wiederherstellen. Beispielsweise FROM DISK = '\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup ".  
  
 *backup_directory*  
 Gibt den Namen eines Verzeichnisses an, die das vollständige oder differenzielle Sicherung enthält. Beispielsweise können Sie eine RESTORE HEADERONLY-Operation für eine vollständige oder differenzielle Sicherung ausführen.  
  
 *full_backup_directory*  
 Gibt den Namen eines Verzeichnisses, das die vollständige Sicherung enthält.  
  
 *differential_backup_directory*  
 Gibt den Namen des Verzeichnisses, das die differenzielle Sicherung enthält.  
  
-   Das Verzeichnis Pfad und der Sicherung muss bereits vorhanden sein und muss als eine vollqualifizierte Universal naming Convention (UNC)-Pfad angegeben werden.  
  
-   Der Pfad zum Sicherungsverzeichnis handelt es sich nicht um einen lokalen Pfad und keinen Ort auf jedem der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance-Knoten.  
  
-   Die maximale Länge des UNC-Pfad und Name der Sicherungsverzeichnis ist 200 Zeichen lang sein.  
  
-   Der Server oder Host muss eine IP-Adresse angegeben werden.  
  
 RESTORE HEADERONLY  
 Gibt an, um nur die Headerinformationen für eine Benutzerdatenbank-Sicherung zurückzugeben. Zwischen anderen Feldern enthält die Kopfzeile der Beschreibungstext für die Sicherung und der Name der Sicherungskopie. Der Name der Sicherungskopie muss nicht den Namen des Verzeichnisses identisch sein, in dem die Sicherungsdateien gespeichert.  
  
 RESTORE HEADERONLY Ergebnisse Standardressource der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY führt. Das Ergebnis hat mehr als 50 Spalten, die nicht alle verwendeten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Eine Beschreibung der Spalten in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RESTORE HEADERONLY führt, finden Sie unter [RESTORE HEADERONLY &#40; Transact-SQL &#41; ](../../t-sql/statements/restore-statements-headeronly-transact-sql.md).  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **CREATE ANY DATABASE** Berechtigung.  
  
 Erfordert ein Windows-Konto die Berechtigung zum Zugreifen auf und aus dem Sicherungsverzeichnis lesen besitzt. Sie müssen auch speichern, den Windows-Kontoname und das Kennwort in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
1.  So überprüfen die Anmeldeinformationen sind bereits vorhanden ist, verwenden Sie [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md).  
  
2.  Verwenden Sie zum Hinzufügen oder aktualisieren Sie die Anmeldeinformationen, [Sp_pdw_add_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md).  
  
3.  So entfernen Sie die Anmeldeinformationen von [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie [Sp_pdw_remove_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 Die RESTORE DATABASE-Befehl führt zu Fehlern in den folgenden Situationen:  
  
-   Der Name der Datenbank bereits vorhanden ist, auf dem Zielgerät. Um dies zu vermeiden, wählen Sie einen eindeutigen Datenbanknamen an, oder löschen Sie die vorhandene Datenbank, bevor Sie die Wiederherstellung ausführen.  
  
-   Es gibt ein ungültiger Satz von Sicherungsdateien im Sicherungsverzeichnis.  
  
-   Die Login-Berechtigungen sind nicht ausreichend, um eine Datenbank wiederherstellen.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]die richtigen Berechtigungen für den Netzwerkspeicherort, an keinen, in dem die Sicherungsdateien gespeichert sind.  
  
-   Die Netzwerkadresse für das Sicherungsverzeichnis ist nicht vorhanden oder ist nicht verfügbar.  
  
-   Es ist nicht genügend Speicherplatz auf dem Serverknoten oder den Knoten "Zugriffssteuerung" ein. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]nicht bestätigt, dass genügend freier Speicherplatz auf dem Gerät vorhanden ist, bevor die Wiederherstellung initiiert. Aus diesem Grund ist es möglich, einen Fehler außerhalb von Speicherplatz während der Ausführung von RESTORE DATABASE-Anweisung zu generieren. Wenn nicht genügend Speicherplatz auftritt, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] die Wiederherstellung wird ein Rollback ausgeführt.  
  
-   Die Ziel-Appliance, zu der die Datenbank wiederhergestellt wird, hat weniger Computerknoten als die Quelle-Appliance, die von der die Datenbank gesichert wurde.  
  
-   Die Wiederherstellung der Datenbank wird von innerhalb einer Transaktion ausgeführt.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]überwacht den Erfolg der datenbankwiederherstellung. Vor dem Wiederherstellen einer differenziellen datenbanksicherung [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] überprüft, ob die vollständige datenbankwiederherstellung wurde erfolgreich abgeschlossen.  
  
 Nach einer Wiederherstellung müssen die Benutzerdatenbank, Datenbank-Kompatibilitätsgrad 120. Dies gilt für alle Datenbanken, unabhängig von ihren ursprünglichen Kompatibilitätsgrad.  
  
 **Wiederherstellen in einer Anwendung mit einer größeren Anzahl von Serverknoten**  
Führen Sie [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) nach dem Wiederherstellen einer Datenbank von einem Gerät mit größerer, da neuverteilung Transaktionsprotokoll vergrößert wird.  

Wiederherstellen einer Sicherung in einer Anwendung mit einer größeren Anzahl von Serverknoten, wächst die Größe der belegten Datenbank relativ zur Anzahl von Compute-Knoten.  
  
Z. B. beim Wiederherstellen einer 60 GB Datenbank von einem 2-Knoten-Gerät (30 GB pro Knoten) in einer Anwendung 6 Knoten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] eine 180 GB-Datenbank (6 Knoten mit 30 GB pro Knoten) auf dem Gerät 6 Knoten erstellt. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Stellt anfänglich 2 Knoten entsprechend die Quellkonfiguration der Datenbank wieder her, und klicken Sie dann die Daten für alle 6 Knoten neu verteilt.  
  
 Nach der Weitergabe enthält jeder Serverknoten weniger tatsächlichen Daten und mehr freien Speicher als jeder Compute-Knoten auf der kleinere Source-Anwendung. Verwenden Sie den zusätzlichen Speicherplatz, um die Datenbank weitere Daten hinzuzufügen. Wenn die wiederhergestellte Datenbank größer ist, als Sie benötigen, können Sie [ALTER DATABASE &#40; Parallel Datawarehouse &#41; ](../../t-sql/statements/alter-database-parallel-data-warehouse.md) zum Verkleinern der Datenbank-Dateigrößen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Für diese Einschränkungen ist die Einheit für die Quelle der Appliance, von dem die Sicherung der Datenbank erstellt wurde, und Zielgerät ist das Gerät, an dem die Datenbank wiederhergestellt wird.  
  
 Wiederherstellen einer Datenbank wird nicht automatisch neu erstellt Statistiken.  
  
 Nur eine Datenbank wiederherstellen oder BACKUP DATABASE-Anweisung kann zu jedem Zeitpunkt auf dem Gerät ausgeführt werden. Wenn mehrere Backup- und Restore-Anweisungen gleichzeitig gesendet werden, die Appliance einer Warteschlange abgelegt und verarbeiten sie eine zu einem Zeitpunkt.  
  
 Sie können nur eine datenbanksicherung Wiederherstellen einer [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Zielgerät, der die gleiche Anzahl und weitere Serverknoten als die Einheit für die Quelle hat. Zielgerät weniger Computerknoten als das Quell-Gerät nicht möglich.  
  
 Sie können keine Sicherung wiederherstellen, die auf eine Anwendung erstellt wurde, SQL Server 2012 PDW-Hardware in einer Anwendung, die SQL Server 2008 R2-Hardware verfügt. Dies gilt auch, wenn das Gerät ursprünglich mit der SQL Server 2008 R2-PDW-Hardware gekauft wurde und jetzt SQL Server 2012 PDW-Software ausgeführt wird.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine exklusive Sperre für das Datenbankobjekt.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-simple-restore-examples"></a>A. Einfache Beispiele für RESTORE  
 Im folgende Beispiel wird eine vollständige Sicherung wiederhergestellt. die `SalesInvoices2013` Datenbank. Die Sicherungsdateien gespeichert sind, der \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full-Verzeichnis. Die SalesInvoices2013-Datenbank kann nicht auf dem Zielgerät bereits vorhanden, oder dieser Befehl schlägt fehl mit Fehler.  
  
```  
RESTORE DATABASE SalesInvoices2013  
FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="b-restore-a-full-and-differential-backup"></a>B. Stellen Sie eine vollständige und differenzielle Sicherung wieder her.  
 Im folgende Beispiel wird eine vollständige, und klicken Sie dann eine differenzielle Sicherung wiederhergestellt, in der Datenbank SalesInvoices2013  
  
 Die vollständige Sicherung der Datenbank wird wiederhergestellt, von der vollständigen Sicherung, die in gespeichert ist die "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full" Verzeichnis. Wenn die Wiederherstellung erfolgreich abgeschlossen wurde, wird die differenzielle Sicherung der SalesInvoices2013-Datenbank wiederhergestellt.  Die differenzielle Sicherung befindet sich in der "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff" Verzeichnis.  
  
```  
RESTORE DATABASE SalesInvoices2013  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH BASE = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
  
```  
  
### <a name="c-restoring-the-backup-header"></a>C. Den Sicherungsheader wiederherstellen  
 In diesem Beispiel wird die Headerinformationen für die datenbanksicherung "\\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full". Der Befehl ergibt sich eine Zeile mit Informationen für die Sicherung Invoices2013Full.  
  
```  
RESTORE HEADERONLY  
    FROM DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full'  
[;]  
```  
  
 Sie können die Headerinformationen verwenden, um den Inhalt einer Sicherung zu überprüfen oder um sicherzustellen, dass das Zielgerät für die Wiederherstellung mit der Quelle backup Appliance kompatibel ist, vor dem Wiederherstellen der Sicherung.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbank sichern &#40; Parallel Datawarehouse &#41;](../../t-sql/statements/backup-database-parallel-data-warehouse.md)  
  
  

