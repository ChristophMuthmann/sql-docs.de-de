---
title: "Protokolldatei-Viewer (F1-Hilfe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "reference"
f1_keywords: 
  - "sql13.swb.configurelogs.errorlog.f1"
helpviewer_keywords: 
  - "Protokolldatei-Viewer"
ms.assetid: 2243845c-4880-4aa0-9ee8-0a97a128996b
caps.latest.revision: 38
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 38
---
# Protokolldatei-Viewer (F1-Hilfe)
  Im Protokolldatei-Viewer können Protokollinformationen aus einer Vielzahl von Komponenten angezeigt werden. Wählen Sie im geöffneten Protokolldatei-Viewer im Bereich **Protokolle auswählen** die Protokolle aus, die angezeigt werden sollen. In jedem Protokoll werden dem Protokolltyp entsprechende Spalten angezeigt.  
  
 Welche Protokolle verfügbar sind, ist davon abhängig, wie der Protokolldatei-Viewer geöffnet wird. Weitere Informationen finden Sie unter [Öffnen des Protokolldatei-Viewers](../../relational-databases/logs/open-log-file-viewer.md).  
  
 Die Anzahl der angezeigten Zeilen für Überwachungsprotokolle kann auf der Seite **SQL Server Objekt-Explorer/Befehle** im Dialogfeld **Extras/Optionen** konfiguriert werden. Beschreibungen der Spalten, die für Überwachungsprotokolle angezeigt werden, finden Sie unter [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md).  
  
## Optionen  
 **Protokoll laden**  
 Öffnen Sie ein Dialogfeld, in dem Sie eine zu ladende Protokolldatei angeben können.  
  
 **Exportieren**  
 Öffnen Sie ein Dialogfeld, in dem Sie die im Raster **Protokolldateizusammenfassung** angezeigten Informationen in eine Textdatei exportieren können.  
  
 **Aktualisieren**  
 Aktualisieren Sie die Anzeige der ausgewählten Protokolle. Beim Übernehmen von Filtereinstellungen werden mithilfe der Schaltfläche **Aktualisieren** die ausgewählten Protokolle erneut vom Zielserver gelesen.  
  
 **Filter**  
 Öffnen Sie ein Dialogfeld, in dem Sie zum Filtern der Protokolldatei verwendete Einstellungen angeben können, z.B. Filterkriterien wie **Verbindung**, **Datum** oder **Allgemein**.  
  
 **Suchen**  
 Durchsuchen Sie die Protokolldatei nach bestimmtem Text. Das Suchen mit Platzhalterzeichen wird nicht unterstützt.  
  
 **Beenden**  
 Beendet das Laden der Protokolldateieinträge. Diese Option können Sie z. B. verwenden, wenn das Laden einer Remote- oder Offline-Protokolldatei eine lange Zeit in Anspruch nimmt und Sie nur die zuletzt erstellten Einträge anzeigen möchten.  
  
 **Protokolldateizusammenfassung**  
 In diesem Informationsbereich wird eine Zusammenfassung der Protokolldateifilterung angezeigt. Wenn die Datei nicht gefiltert wurde, wird folgender Text angezeigt: **Kein Filter angewendet**. Nach Anwendung eines Filters auf das Protokoll wird folgender Text angezeigt: **Protokolleinträge auf diesen Fall filtern:** \<Filterkriterien>.  
  
 **Details für die ausgewählte Zeile**  
 Wählen Sie eine Zahl aus, um am unteren Rand der Seite zusätzliche Details zu der ausgewählten Ereigniszeile anzuzeigen. Die Spalten können durch Ziehen an neue Positionen im Raster neu angeordnet werden. Die Breite der Spalten kann durch Ziehen der Spaltentrennbalken in der Kopfzeile des Rasters nach links oder rechts geändert werden. Wenn Sie auf die Spaltentrennbalken in der Kopfzeile des Rasters doppelklicken, wird die Breite der Spalte automatisch an die Breite des Inhalts angepasst.  
  
 **Instanz**  
 Der Name der Instanz, bei der das Ereignis aufgetreten ist. Dieser wird im Format *Computername*\\*Instanzname*.  
  
## Häufig angezeigte Spalten  
 **Datum**  
 Zeigt das Datum des Ereignisses an.  
  
 **Quelle**  
 Zeigt die Ausgangsfunktion an, mit dem das Ereignis erstellt wurde, z. B. den Namen des Diensts (z. B. MSSQLSERVER). Dies wird nicht für alle Protokolltypen angezeigt.  
  
 **MessageBox**  
 Zeigt die Meldungen an, die dem Ereignis zugeordnet sind.  
  
 **Protokolltyp**  
 Zeigt den Typ des Protokolls an, zu dem das Ereignis gehört. Alle ausgewählten Protokolle werden im Fenster für die Protokolldateizusammenfassung angezeigt.  
  
 **Protokollquelle**  
 Zeigt eine Beschreibung des Quellprotokolls an, in dem das Ereignis aufgezeichnet wird.  
  
## Berechtigungen  
 Zum Zugreifen auf Protokolldateien für Onlineinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sie Mitglied der festen Serverrolle „securityadmin“ sein.  
  
 Zum Zugreifen auf Protokolldateien für Offlineinstanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] müssen Sie über Lesezugriff für den WMI-Namespace **Root\Microsoft\SqlServer\ComputerManagement10** und den Ordner mit den Protokolldateien verfügen. Weitere Informationen finden Sie im Abschnitt „Sicherheit“ des Themas [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md).  
  
## Siehe auch  
 [Protokolldatei-Viewer](../../relational-databases/logs/log-file-viewer.md)   
 [Öffnen des Protokolldatei-Viewers](../../relational-databases/logs/open-log-file-viewer.md)   
 [Anzeigen von Offlineprotokolldateien](../../relational-databases/logs/view-offline-log-files.md)  
  
  