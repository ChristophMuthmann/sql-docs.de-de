---
title: Erwerben und einen Sicherungsserver - Parallel Data Warehouse konfigurieren | Microsoft Docs
description: Dieser Artikel beschreibt, wie einem nicht-Appliance-Windows-Betriebssystem als Sicherungsserver für die Verwendung mit die Sicherung und Wiederherstellung Funktionen Analytics Platform System (APS) und Parallel Data Warehouse (PDW) konfigurieren.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 4464857e2b1e71a96f87e95d45df0577df987176
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/19/2018
---
# <a name="acquire-and-configure-a-backup-server-for-parallel-data-warehouse"></a>Erwerben Sie und konfigurieren Sie einen Sicherungsserver für Parallel Data Warehouse
Dieser Artikel beschreibt, wie einem nicht-Appliance-Windows-Betriebssystem als Sicherungsserver für die Verwendung mit die Sicherung und Wiederherstellung Funktionen Analytics Platform System (APS) und Parallel Data Warehouse (PDW) konfigurieren.  
  
  
## <a name="Basics"></a>Grundlagen der Backup-server  
Die backup-Server:  
  
-   Bereitgestellt und von Ihr IT-Team verwaltet wird.  
  
-   PDW-spezifische Software oder Tools ist nicht erforderlich. PDW wird Software auf dem backup-Server nicht installiert.  
  
-   Befindet sich in Ihrem eigenen nicht-Appliance Gestell und kann nicht in der APS-Einheit platziert werden.  
  
-   Kann mit dem Gerät InfiniBand-Netzwerk verbunden werden. Sicherungen können über InfiniBand oder Ethernet ausgeführt werden; InfiniBand wird aus Leistungsgründen empfohlen.  
  
-   Befindet sich in Ihren eigenen Kundendomäne nicht der Domäne der Anwendung. Es ist keine Vertrauensstellung zwischen Ihrer Kunden und der Appliance-Domäne ein.  
  
-   Hostet eine Sicherungsdatei-Freigabe, die eine Windows-Dateifreigabe ist das Netzwerkprotokoll für Server Message Block (SMB) auf Anwendungsebene verwendet. Die Freigabeberechtigungen für die Sicherungsdatei geben ein Windows-Domänenbenutzer (in der Regel ist dies ein dedizierter backup Benutzer) die Möglichkeit zum Ausführen der Sicherung und Wiederherstellungsvorgänge auf die Freigabe. Der Benutzername und Kennwort-Anmeldeinformationen des Windows-Domänenbenutzer sind in PDW gespeichert, sodass PDW Sicherung durchführen und Wiederherstellungsvorgänge auf der sicherungsdateifreigabe kann.  
  
## <a name="Step1"></a>Schritt 1: Ermitteln der Kapazitätsanforderungen  
Die Systemanforderungen für den Backup-Server hängt der eigenen arbeitsauslastung, fast vollständig. Vor dem Kauf oder einen backup-Server-Bereitstellung müssen Sie die kapazitätsanforderungen zu ermitteln. Die Backup-Server muss nicht nur für Sicherungen, dedizierten werden, solange sie die Leistung und Speicher die Anforderungen Ihrer arbeitsauslastung behandelt. Sie können auch veranlassen, dass mehrere Sicherungsserver zum Sichern und Wiederherstellen jeder Datenbank auf einen von mehreren Servern.  
  
Verwenden der [Planung Arbeitsblatt des Backup-Kapazität](backup-capacity-planning-worksheet.md) feststellen, dass die kapazitätsanforderungen.  
  
## <a name="Step2"></a>Schritt 2: Abrufen eines den backup-server  
Nun, dass Sie die kapazitätsanforderungen besser verstehen, können Sie planen, die Server und Netzwerkkomponenten, die Sie zum Erwerb oder bereitstellen müssen. Integrieren Sie, die folgende Liste von Anforderungen für Ihren Einkauf Plan und erwerben Sie den Server zu oder Bereitstellen Sie einen vorhandenen Server.  
  
### <a name="software-requirements"></a>Softwareanforderungen  
Alle Dateiserver, die das Windows-Datei Freigabe (SMB)-Protokoll verwendet.  
  
Wir empfehlen, dass Windows Server 2012 oder darüber hinaus in der Reihenfolge auf:  
  
-   Abrufen des Leistungsvorteil Datei Vorabbelegung über SMB.  
  
-   Verwenden Sie für Sicherungsvorgänge Instant Datei Initialisierung (IFI). Ihr IT-Team wird diese Einstellung auf dem backup-Server verwaltet. Die PDW-Konfigurations-Manager (dwconfig.exe) nicht festgelegt oder IFI steuern, auf dem backup-Server. Frühere Versionen von Windows keinen IFI aber immer noch als Sicherungsserver verwendet werden können.  
  
### <a name="networking-requirements"></a>Netzwerkanforderungen  
Obwohl nicht erforderlich ist, ist InfiniBand für Backup-Server den empfohlenen Verbindungstyp. Vorbereiten für den Server Laden mit dem Appliance InfiniBand-Netzwerk verbinden:  
  
1.  Planen den Server im rack aus, um das Gerät, damit Sie das Gerät hergestellt werden können InfiniBand-switches zu schließen. Weitere Informationen über Mellanox-Technologien InfiniBand, finden Sie im Whitepaper [Einführung in InfiniBand](http://www.mellanox.com/pdf/whitepapers/IB_Intro_WP_190.pdf).  
  
2.  Erwerben Sie einen Netzwerkadapter für Mellanox ConnectX-3 FDR InfiniBand und duale Port. Es wird empfohlen, erwerben den Netzwerkadapter mit zwei Ports für die Fehlertoleranz während der Datenübertragung. Ein Netzwerkadapter zwei Port ist für hohe Verfügbarkeit erforderlich.  
  
3.  Erwerben Sie 2 FDR InfiniBand-Kabel für eine dual-Port-Karte oder 1 FDR InfiniBand-Kabel für einen einzelnen Port-Karte. Die FDR InfiniBand-Kabel verbindet den Server Laden mit dem Gerät InfiniBand-Netzwerk. Die Länge der Kabel hängt von den Abstand zwischen dem Server geladen und die Einheiten InfiniBand-Switches, entsprechend Ihrer Umgebung ab.  
  
## <a name="Step3"></a>Schritt 3: Verbinden Sie den Server mit InfiniBand-Netzwerke  
Gehen Sie folgendermaßen vor, um den Server Laden mit dem InfiniBand-Netzwerk zu verbinden. Wenn der Server das InfiniBand-Netzwerk nicht verwendet wird, überspringen Sie diesen Schritt.  
  
1.  Rack Server schließen genug, um das Gerät, damit Sie die Appliance InfiniBand-Netzwerk hergestellt werden können.  
  
2.  Installieren Sie den InfiniBand Mellanox ConnectX-3 FDR InfiniBand-Netzwerkadapter in den Server geladen.  
  
3.  Verwenden Sie die FDR-Kabel, um InfiniBand-Netzwerkadapter mit einer der zwei InfiniBand-Schalter in der ersten Appliance Rack herstellen.  
  
4.  Installieren Sie und konfigurieren Sie den entsprechenden Windows-Treiber für den InfiniBand-Netzwerkadapter.  
  
    -   InfiniBand-Treiber für Windows sind von der OpenFabrics Alliance, einer Branche Consortium InfiniBand-Hersteller entwickelt.  Der richtige Treiber möglicherweise mit dem InfiniBand-Netzwerkadapter verteilt wurden. Wenn dies nicht der Fall ist, wird der Treiber kann von www.openfabrics.org heruntergeladen werden.  
  
5.  Konfigurieren Sie InfiniBand und DNS-Einstellungen für die Netzwerkadapter. Anweisungen zur Konfiguration finden Sie unter [InfiniBand-Netzwerkadapter konfigurieren](configure-infiniband-network-adapters.md).  
  
## <a name="Step4"></a>Schritt 4: Konfigurieren der sicherungsdateifreigabe  
PDW greifen über eine UNC-Dateifreigabe auf den backup-Server zu. So richten die Dateifreigabe  
  
1.  Erstellen Sie einen Ordner auf dem backup-Server zum Speichern von Sicherungen.  
  
2.  Erstellen Sie eine Dateifreigabe, eine Sicherungsfreigabe fest, für den Sicherungsordner aufgerufen.  
  
3.  Oder erstellen Sie ein Windows-Domänenkonto in der Customer-Domäne, die im Rahmen der Ausführung von Sicherungen und Wiederherstellungen verwendet werden sollen. Aus Sicherheitsgründen empfiehlt es sich um ein dediziertes Konto als backup-Benutzer verwenden.  
  
4.  Fügen Sie Berechtigungen für die Sicherung Teilen, sodass nur vertrauenswürdigen Konten und eine Sicherung Domänenkonto zugreifen können, lesen und Schreiben in den Speicherort der Dateifreigabe ein.  
  
5.  Fügen Sie den Anmeldeinformationen des Domänenkontos backup mit PDW hinzu.  
  
    Beispiel:  
  
    ```sql  
    EXEC sp_pdw_add_network_credentials '10.192.147.63', 'seattle\david', '********';  
    ```  
  
    Weitere Informationen finden Sie diese gespeicherten Prozeduren aus:  
  
    -   [sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
    -   [sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
## <a name="Step5"></a>Schritt 5: Starten Sie Ihre Daten sichern  
Sie können nun das Sichern von Daten mit dem backup-Server.  
  
Die Daten sichern, verwenden Sie einen Abfrage-Client eine Verbindung mit SQL Server PDW und senden Sie BACKUP DATABASE oder RESTORE DATABASE-Befehle. Verwenden Sie den Datenträger =-Klausel zum Angeben des Speicherorts Sicherung, Server und die Sicherung.  
  
> [!IMPORTANT]  
> Denken Sie daran, die InfiniBand IP-Adresse des dem backup-Server verwenden. Andernfalls werden die Daten über Ethernet statt InfiniBand kopiert.  
  
Beispiel:  
  
```sql  
BACKUP DATABASE Invoices TO DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full';  
  
RESTORE DATABASE Invoices2013Full  
FROM DISK = '\\10.172.14.255\backups\yearly\Invoices2013Full'  
```  
  
Weitere Informationen finden Sie in den folgenden Themen: 
  
-   [BACKUP DATABASE](../t-sql/statements/backup-database-parallel-data-warehouse.md)   
  
-   [STELLEN SIE DIE DATENBANK WIEDER HER.](../t-sql/statements/restore-database-parallel-data-warehouse.md)  
  
## <a name="Security"></a>Sicherheit-Hinweise  
Der backup-Server ist nicht für die Anwendung der privaten Domäne verknüpft. Es ist in Ihrem eigenen Netzwerk, und es besteht keine Vertrauensstellung zwischen Ihrer eigenen Domäne und privaten Appliance-Domäne.  
  
Da PDW Sicherungen nicht auf dem Gerät gespeichert werden, ist Ihr IT-Team zuständig für das Verwalten aller Aspekte der backup-Sicherheit. Beispielsweise schließt dies Verwalten der Sicherheit von Sicherungsdaten, die Sicherheit des Servers, der zum Speichern von Sicherungen verwendet und die Sicherheit der Netzwerkinfrastruktur, die der Sicherung in der APS-Anwendung eine Verbindung herstellt.  
  
### <a name="manage-network-credentials"></a>Verwalten von Anmeldeinformationen für das Netzwerk  
  
Der Netzwerkzugriff auf das Sicherungsverzeichnis basiert auf der Windows-Standarddateifreigabesicherheit. Bevor Sie eine Sicherung ausführen, müssen Sie erstellen oder reservieren Sie ein Windowskonto, das zum Authentifizieren von PDW im Sicherungsverzeichnis verwendet werden soll. Dieses Windows-Konto benötigt die Berechtigung, auf das Sicherungsverzeichnis zuzugreifen, es zu erstellen und auf es zu schreiben.  
  
> [!IMPORTANT]  
> Um Sicherheitsrisiken in Verbindung mit Ihren Daten zu reduzieren, empfehlen wir, dass Sie ein Windows-Konto ausschließlich zum Ausführen der Sicherungs- und Wiederherstellungsvorgänge festlegen. Definieren Sie das Konto so, dass es nur Berechtigungen für den Sicherungsspeicherort besitzt.  
  
Um den Benutzernamen und das Kennwort im PDW speichern möchten, verwenden Sie die [Sp_pdw_add_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md) gespeicherte Prozedur. PDW verwendet Windows-Anmeldeinformationsverwaltung zum Speichern und Verschlüsseln von Benutzernamen und Kennwörter auf den Knoten "Zugriffssteuerung" und Compute-Knoten. Die Anmeldeinformationen werden nicht mit dem Befehl BACKUP DATABASE gesichert.  
  
Verwenden Sie zum Entfernen der Anmeldeinformationen für das Netzwerk aus PDW die [Sp_pdw_remove_network_credentials](../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md) gespeicherte Prozedur.  
  
Um alle in SQL Server PDW gespeicherten Anmeldeinformationen für das Netzwerk aufzulisten, verwenden Sie die [sys.dm_pdw_network_credentials](../relational-databases/system-dynamic-management-views/sys-dm-pdw-network-credentials-transact-sql.md) -verwaltungssicht.  
  
### <a name="secure-communications"></a>Sichere Kommunikation  
  
Vorgänge auf dem Server laden können einen UNC-Pfad, um Daten von außerhalb des vertrauenswürdigen internen Netzwerks verwenden. Ein Angreifer im Netzwerk oder mit der Möglichkeit, die namensauflösung beeinflussen kann abzufangen oder zu an die PDW gesendete Daten ändern. Dies stellt ein Risiko der Offenlegung von Manipulationen und Informationen. Um das Risiko von Manipulationen zu verringern:

- Machen Sie Signierung von für die Verbindung erforderlich. 
- Legen Sie auf dem Server Laden der folgenden Gruppe Richtlinienoption in Security-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\sicherheitsoptionen: Microsoft-Netzwerkclient: Kommunikation digital signieren (immer): aktiviert.  
  
## <a name="see-also"></a>Siehe auch  
[Sichern und Wiederherstellen](backup-and-restore-overview.md)  
  
