---
title: SICHERUNGSDATENBANK (Parallel Datawarehouse) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 73c8d465-b36b-4727-b9f3-368e98677c64
caps.latest.revision: 11
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4fb36fd89c02ff9ddd5bc33825a387b53ab6e174
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="backup-database-parallel-data-warehouse"></a>SICHERUNGSDATENBANK (Parallel Datawarehouse)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw_md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  Erstellt eine Sicherungskopie der eine [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank und speichert die Sicherung deaktiviert das Gerät in einem Benutzer angegebenen Netzwerkadresse. Verwenden Sie diese Anweisung mit [Datenbank wiederherstellen &#40; Parallel Datawarehouse &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) Wiederherstellung im Notfall oder eine Datenbank auf einem Gerät in einen anderen kopieren.  
  
 **Vor dem Beginn**, finden Sie unter "Abrufen und Konfigurieren eines Server sichern" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 Es gibt zwei Arten von Sicherungen in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Ein *vollständige datenbanksicherung* ist eine Sicherung einer gesamten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Datenbank. Ein *differenziellen* umfasst nur Änderungen seit der letzten vollständigen Sicherung vorgenommen wurden. Eine Sicherung einer Benutzerdatenbank umfasst Datenbankbenutzer und Datenbankrollen. Eine Sicherung der master-Datenbank umfasst Anmeldungen.  
  
 Weitere Informationen zu [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] datenbanksicherungen, finden Sie unter "Sichern und Wiederherstellen" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 ![Symbol für Themenlink](../../database-engine/configure-windows/media/topic-link.gif "Thema Linksymbol") [Transact-SQL-Syntaxkonventionen &#40; Transact-SQL &#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
      Create a full backup of a user database or the master database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    [ WITH [ ( ]  <with_options> [ ,...n ]  [ ) ] ]  
[;]  
  
Create a differential backup of a user database.  
BACKUP DATABASE database_name  
    TO DISK = '\\UNC_path\backup_directory'  
    WITH [ ( ] DIFFERENTIAL   
    [ , <with_options> [ ,...n ] [ ) ]  
[;]  
  
<with_options> ::=  
    DESCRIPTION = 'text'  
    | NAME = 'backup_name'  
  
```  
  
## <a name="arguments"></a>Argumente  
 *database_name*  
 Der Name der Datenbank auf dem eine Sicherung erstellt. Die Datenbank kann es sich um die master-Datenbank oder eine Benutzerdatenbank sein.  
  
 AUF den Datenträger = "\\\\*UNC_path*\\*Backup_directory*"  
 Der Netzwerkpfad und das Verzeichnis, in dem [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] schreibt die Sicherungsdateien. Z. B. "\\\xxx.xxx.xxx.xxx\backups\2012\Monthly\08.2012.Mybackup".  
  
-   Der Pfad zur Sicherungsverzeichnis Namen muss bereits vorhanden und muss als eine vollqualifizierte Universal naming Convention (UNC)-Pfad angegeben werden.  
  
-   Das Sicherungsverzeichnis *Backup_directory*, darf nicht vor dem Ausführen des Sicherungsbefehls vorhanden sein. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]erstellt das Sicherungsverzeichnis.  
  
-   Der Pfad zum Sicherungsverzeichnis handelt es sich nicht um einen lokalen Pfad und keinen Ort auf jedem der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance-Knoten.  
  
-   Die maximale Länge des UNC-Pfad und Name der Sicherungsverzeichnis ist 200 Zeichen lang sein.  
  
-   Der Server oder Host muss eine IP-Adresse angegeben werden.  Sie können nicht als Host-oder Server angeben.  
  
 DESCRIPTION = **"***Text***"**  
 Gibt eine Beschreibung des Sicherungssatzes an. Die maximale Länge des Texts beträgt 255 Zeichen.  
  
 Die Beschreibung wird in den Metadaten gespeichert und wird angezeigt, wenn der Sicherungsheader mit RESTORE HEADERONLY wiederhergestellt wird.  
  
 NAME = **"***backup _name***"**  
 Gibt den Namen des Sicherungssatzes. Der Name der Sicherungskopie kann anhand des Datenbanknamens abweichen.  
  
-   Namen können maximal 128 Zeichen haben.  
  
-   Einen Pfad einschließen  
  
-   Muss mit einem Buchstaben oder einer Ziffer Zeichen oder einem Unterstrich (_) beginnen. Sonderzeichen, die zulässig sind, den Unterstrich (\_), Bindestrich (-) oder Leerzeichen (). Sicherungsnamen darf nicht mit einem Leerzeichen enden.  
  
-   Die Anweisung schlägt fehl, wenn *Backup_name* am angegebenen Speicherort bereits vorhanden ist.  
  
 Dieser Name wird in den Metadaten gespeichert und wird angezeigt, wenn der Sicherungsheader mit RESTORE HEADERONLY wiederhergestellt wird.  
  
 DIFFERENTIAL  
 Gibt an, dass eine differenzielle Sicherung einer Benutzerdatenbank. Wenn nicht angegeben, ist die Standardeinstellung eine vollständige Sicherung aus. Der Name der differenziellen Sicherung muss nicht mit dem Namen der vollständigen Sicherung übereinstimmen. Zum Nachverfolgen der differenziellen Sicherung und die zugehörige vollständige Sicherung, erwägen Sie den gleichen Namen mit "full" oder "momentaufnahmevergleich" angefügt.  
  
 Beispiel:  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerFull';`  
  
 `BACKUP DATABASE Customer TO DISK = '\\xxx.xxx.xxx.xxx\backups\CustomerDiff' WITH DIFFERENTIAL;`  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die **BACKUP DATABASE** Berechtigung oder die Mitgliedschaft in der **Db_backupoperator** festen Datenbankrolle "". Der master-Datenbank kann nicht gesichert werden, sich jedoch durch ein normaler Benutzer das hinzugefügte der **Db_backupoperator** festen Datenbankrolle "". Der master-Datenbank kann nur gesichert werden durch **sa**die Fabric-Administrator oder Mitglied der **Sysadmin** festen Serverrolle "".  
  
 Erfordert ein Windowskonto, das über die Berechtigung den Zugriff, erstellen und Schreiben im Sicherungsverzeichnis verfügt. Sie müssen auch speichern, den Windows-Kontoname und das Kennwort in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]. Diese Anmeldeinformationen für das Netzwerk zum Hinzufügen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie die [Sp_pdw_add_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) gespeicherte Prozedur.  
  
 Weitere Informationen zum Verwalten von Anmeldeinformationen in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], finden Sie unter der [Sicherheit](#Security) Abschnitt.  
  
## <a name="error-handling"></a>Fehlerbehandlung  
 BACKUP DATABASE-Fehler in den folgenden Situationen:  
  
-   Berechtigungen sind nicht ausreichend, um eine Sicherung auszuführen.  
  
-   [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]die richtigen Berechtigungen für den Netzwerkspeicherort, an keinen, in dem die Sicherung gespeichert wird.  
  
-   Die Datenbank ist nicht vorhanden.  
  
-   Das Zielverzeichnis ist bereits vorhanden, auf der Netzwerkfreigabe.  
  
-   Die Ziel-Netzwerkfreigabe ist nicht verfügbar.  
  
-   Die Ziel-Netzwerkfreigabe besitzt nicht genügend Speicherplatz für die Sicherung. Der BACKUP DATABASE-Befehl bestätigt nicht, dass genügend freier Speicherplatz vorhanden ist, vor dem Initiieren der Sicherung, wodurch Fehler Out of Disk Space zu generieren, während der Ausführung der BACKUP DATABASE. Wenn nicht genügend Speicherplatz auftritt, [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] wird durch ein Rollback der BACKUP DATABASE-Befehl. Führen Sie zum Verringern der Größe Ihrer Datenbank [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md)  
  
-   Der Versuch, eine Sicherung innerhalb einer Transaktion zu starten.  
  
## <a name="general-remarks"></a>Allgemeine Hinweise  
 Verwenden Sie vor dem Ausführen einer datenbanksicherung [DBCC SHRINKLOG (Azure SQL Data Warehouse)](../../t-sql/database-console-commands/dbcc-shrinklog-azure-sql-data-warehouse.md) zum Verringern der Größe der Datenbank. 
 
 Ein [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Sicherung wird als eine Reihe von mehreren Dateien im gleichen Verzeichnis gespeichert.  
  
 Eine differenzielle Sicherung normalerweise weniger Zeit als eine vollständige Sicherung und häufiger ausgeführt werden kann. Wenn mehrere differenzielle Sicherungen auf der gleichen vollständigen Sicherung basieren, enthält jeder differenziellen Sicherung aller Änderungen in der vorherigen differenziellen Sicherung.  
  
 Wenn Sie einen BACKUP-Befehl Abbrechen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] entfernt das Zielverzeichnis und alle Dateien, die für die Sicherung erstellt wurde. Wenn [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] verliert Netzwerkkonnektivität auf die Freigabe das Rollback kann nicht abgeschlossen werden.  
  
 Vollständige und differenzielle Sicherungen werden in separaten Verzeichnissen gespeichert. Durch Benennungskonventionen werden nicht erzwungen, zum angeben, dass eine vollständige Sicherung und eine differenzielle Sicherung zusammengehören. Sie können diese über Ihre eigenen Benennungskonventionen nachverfolgen. Alternativ können Sie dies mithilfe der mit Beschreibung-Option verwenden, um eine Beschreibung hinzuzufügen, und klicken Sie dann mithilfe von RESTORE HEADERONLY-Anweisung zum Abrufen der Beschreibung nachverfolgen.  
  
## <a name="limitations-and-restrictions"></a>Einschränkungen  
 Eine differenzielle Sicherung der master-Datenbank ist nicht möglich. Es werden nur vollständige Sicherungen der master-Datenbank unterstützt.  
  
 Die Sicherungsdateien gespeichert sind, in einem Format geeignet ist nur für die Wiederherstellung der Sicherung auf einen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance mithilfe der [Datenbank wiederherstellen &#40; Parallel Datawarehouse &#41; ](../../t-sql/statements/restore-database-parallel-data-warehouse.md) Anweisung.  
  
 Die Sicherung mit der BACKUP DATABASE-Anweisung kann nicht verwendet werden, um Daten oder Benutzerinformationen in SMP übertragen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Datenbanken. Für diese Funktion können Sie die Remotetabelle Copy-Funktion verwenden. Weitere Informationen finden Sie unter "Remote Tabelle kopieren" in der [!INCLUDE[pdw-product-documentation](../../includes/pdw-product-documentation-md.md)].  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]verwendet [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Technologie sichern und Wiederherstellen von Datenbanken zu sichern. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Backup-Optionen sind vorkonfiguriert, um die Komprimierung von Sicherungen verwenden. Sie können keine Sicherungsoptionen z. B. Komprimierung, Checksum-Blockgröße und Puffergröße festlegen.  
  
 Nur eine Sicherung oder Wiederherstellung kann auf das Gerät zu einem beliebigen Zeitpunkt ausführen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Backup oder Restore-Befehlen bis zur aktuellen Sicherung Warteschlange oder Restore-Befehl wurde abgeschlossen.  
  
 Zielgerät für die Sicherung wiederherstellt, muss als die Quelle Appliance mindestens so viele Computeknoten umfassen. Das Ziel kann weitere Serverknoten als die Quelle Appliance, aber keine weniger Computerknoten.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]wird nicht verfolgt den Speicherort und Namen von Sicherungen, da die Sicherungen gespeichert sind, deaktiviert die Appliance.  
  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Hierbei kann es sich um den Erfolg oder Misserfolg von datenbanksicherungen nachverfolgen.  
  
 Eine differenzielle Sicherung ist nur zulässig, wenn die letzte vollständige Sicherung erfolgreich abgeschlossen wurde. Nehmen wir beispielsweise an, dass am Montag, die Sie einer vollständigen Sicherung der Sales-Datenbank erstellen und die Sicherung erfolgreich abgeschlossen wird. Klicken Sie dann am Dienstag, die Sie Erstellen einer vollständigen Sicherung der Sales-Datenbank, und ein Fehler auftritt. Nach diesem Fehler können nicht Sie eine differenzielle Sicherung basierend auf vom Montag vollständige Sicherung erstellen. Sie müssen zuerst eine vollständige Sicherung vor dem Erstellen einer differenziellen Sicherung erstellen.  
  
## <a name="metadata"></a>Metadaten  
 Diese dynamischen Verwaltungssichten enthalten Informationen über alle Sicherung, Wiederherstellung und Ladevorgänge. Die Informationen, die über Systemneustarts weiterhin besteht.  
  
-   [Sys.pdw_loader_backup_runs &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [Sys.pdw_loader_backup_run_details &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
-   [Sys.pdw_loader_run_stages &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md)  
  
## <a name="performance"></a>Leistung  
 Zum Ausführen einer Sicherung [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] erste sichert die Metadaten, und klicken Sie dann führt eine parallele Sicherung der Datenbankdaten auf den Serverknoten gespeichert. Daten werden direkt aus jeder Serverknoten im Sicherungsverzeichnis kopiert. Die beste Leistung zum Verschieben von Daten von den Computeknoten im Sicherungsverzeichnis erzielen [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] steuert die Anzahl von Serverknoten, die gleichzeitig von Daten kopieren.  
  
## <a name="locking"></a>Sperren  
 Akzeptiert eine ExclusiveUpdate-Sperre für das Datenbankobjekt.  
  
##  <a name="Security"></a> Sicherheit  
 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Sicherungen werden nicht auf dem Gerät gespeichert. Daher ist Ihr IT-Team zuständig für das Verwalten aller Aspekte der backup-Sicherheit. Dies beinhaltet die Verwaltung der Sicherheit der Sicherungsdaten, die Sicherheit des Servers, der zum Speichern von Sicherungen verwendet und die Sicherheit der Netzwerkinfrastruktur, die der Sicherung um eine Verbindung herstellt der [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] Appliance.  
  
 **Verwalten von Anmeldeinformationen für das Netzwerk**  
  
 Netzwerkzugriff auf das Sicherungsverzeichnis basiert auf standard Sicherheit der Windows-Dateifreigabe. Vor dem Ausführen einer Sicherung, müssen Sie erstellen oder reservieren Sie ein Windows-Konto für die Authentifizierung verwendeten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] auf das Sicherungsverzeichnis. Dieses Windows-Konto muss über die Berechtigung den Zugriff, erstellen und Schreiben im Sicherungsverzeichnis.  
  
> [!IMPORTANT]  
>  Um Sicherheitsrisiken mit Ihren Daten zu reduzieren, empfehlen wir, dass Sie ein Windows-Konto ausschließlich zum Zweck der Sicherung festlegen und Wiederherstellungsvorgänge. Ermöglichen Sie diesem Konto Berechtigungen für den Sicherungsspeicherort, und an keiner anderen Stelle verfügen.  
  
 Sie müssen den Benutzernamen und Kennwort in speichern [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] durch Ausführen der [Sp_pdw_add_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) gespeicherte Prozedur. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]Windows-Anmeldeinformationsverwaltung wird zum Speichern und Verschlüsseln von Benutzernamen und Kennwörter auf dem Knoten "Zugriffssteuerung" und Compute-Knoten verwendet. Die Anmeldeinformationen sind nicht mit dem Befehl BACKUP DATABASE gesichert.  
  
 So entfernen Sie die Anmeldeinformationen für das Netzwerk aus [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], finden Sie unter [Sp_pdw_remove_network_credentials &#40; SQL Datawarehouse &#41; ](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md).  
  
 So Listen Sie alle Anmeldeinformationen für das Netzwerk in gespeicherten [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie die [sys.dm_pdw_network_credentials &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) -verwaltungssicht.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-add-network-credentials-for-the-backup-location"></a>A. Fügen Sie der Netzwerkanmeldeinformationen für den Sicherungsspeicherort  
 So erstellen Sie eine Sicherung [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] benötigen Lese-/Schreibberechtigung für das Sicherungsverzeichnis. Im folgende Beispiel wird gezeigt, wie die Anmeldeinformationen für einen Benutzer hinzuzufügen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]werden diese Anmeldeinformationen zu speichern und verwenden sie für die Sicherung und Wiederherstellungsvorgänge.  
  
> [!IMPORTANT]  
>  Aus Sicherheitsgründen wird empfohlen, mindestens ein Domänenkonto ausschließlich zum Zweck der Durchführung von Sicherungen zu erstellen.  
  
```  
EXEC sp_pdw_add_network_credentials 'xxx.xxx.xxx.xxx', 'domain1\backupuser', '*****';  
```  
  
### <a name="b-remove-network-credentials-for-the-backup-location"></a>B. Entfernen Sie die Anmeldeinformationen für das Netzwerk für den Sicherungsspeicherort  
 Im folgende Beispiel wird gezeigt, wie zum Entfernen der Anmeldeinformationen für ein Domänenbenutzerkonto aus [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
```  
EXEC sp_pdw_remove_network_credentials 'xxx.xxx.xxx.xxx';  
```  
  
### <a name="c-create-a-full-backup-of-a-user-database"></a>C. Erstellen Sie eine vollständige Sicherung einer Benutzerdatenbank  
 Das folgende Beispiel erstellt eine vollständige Sicherung der Benutzerdatenbank Rechnungen. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]erstellt das Verzeichnis Invoices2013 und speichert die Sicherungsdateien der \\\10.192.63.147\backups\yearly\Invoices2013Full-Verzeichnis.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Full';  
```  
  
### <a name="d-create-a-differential-backup-of-a-user-database"></a>D. Erstellen einer differenziellen Sicherung einer Benutzerdatenbank  
 Das folgende Beispiel erstellt eine differenzielle Sicherung, die alle Änderungen seit der letzten vollständigen Sicherung der Datenbank Rechnungen enthält. [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]erstellt die \\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff-Verzeichnis, dem die Dateien speichert. Die Beschreibung "Rechnungen 2013 differenzielle Sicherung" wird mit der Headerinformationen für die Sicherung gespeichert werden.  
  
 Die differenzielle Sicherung wird nur erfolgreich ausgeführt werden, wenn die letzte vollständige Sicherung von Rechnungen erfolgreich abgeschlossen wurde.  
  
```  
BACKUP DATABASE Invoices TO DISK = '\\xxx.xxx.xxx.xxx\backups\yearly\Invoices2013Diff'  
    WITH DIFFERENTIAL,   
    DESCRIPTION = 'Invoices 2013 differential backup';  
```  
  
### <a name="e-create-a-full-backup-of-the-master-database"></a>E. Erstellen Sie eine vollständige Sicherung der master-Datenbank  
 Im folgenden Beispiel wird eine vollständige Sicherung der master-Datenbank erstellt und speichert ihn in das Verzeichnis "\\\10.192.63.147\backups\2013\daily\20130722\master".  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master';  
```  
  
### <a name="f-create-a-backup-of-appliance-login-information"></a>F. Erstellen Sie eine Sicherung der Appliance-Anmeldeinformationen ein.  
 Der master-Datenbank speichert die Anmeldeinformationen für die Appliance. Um die Anmeldeinformationen für die Anwendung zu sichern, müssen Sie backup Master.  
  
 Das folgende Beispiel erstellt eine vollständige Sicherung der master-Datenbank.  
  
```  
BACKUP DATABASE master TO DISK = '\\xxx.xxx.xxx.xxx\backups\2013\daily\20130722\master'  
WITH (   
    DESCRIPTION = 'Master Backup 20130722',  
    NAME = 'login-backup'  
)  
;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [WIEDERHERSTELLUNGSDATENBANK &#40; Parallel Datawarehouse &#41;](../../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
  

