---
title: "Konfigurieren des Verwaltungs-Data Warehouses (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.dc.datacollection.wizard_completecfg.f1"
  - "sql13.swb.dc.datacollection.wizard_config.f1"
  - "sql13.swb.dc.datacollection.wizard_finish.f1"
  - "sql13.swb.dc.datacollection.wizard_maploginuser.f1"
  - "sql13.swb.dc.datacollection.wizard_choosemdw.f1"
  - "sql13.swb.dc.datacollection.wizard_welcome.f1"
  - "sql13.swb.dc.datacollection.wizard_createmdw.f1"
helpviewer_keywords: 
  - "Data Warehouse [SQL Server], mehrere Instanzen"
  - "Data Warehouse [SQL Server], konfigurieren"
  - "Assistent für die Konfiguration des Verwaltungs-Data Warehouses"
  - "Verwaltungs-Data Warehouse, konfigurieren"
ms.assetid: 23a584f3-c5e1-414c-9afe-73cd7efbda4b
caps.latest.revision: 28
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 28
---
# Konfigurieren des Verwaltungs-Data Warehouses (SQL Server Management Studio)
  In diesem Thema wird beschrieben, wie Sie das Verwaltungs-Data Warehouse für die Unterstützung der Datenspeicherung für einzelne oder mehrere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzen, die den Datensammler verwenden, konfigurieren müssen Diese Instanzen können sich auf dem gleichen Server oder auf verschiedenen Servern befinden. In diesem Thema sind auch Beschreibungen der Benutzeroberfläche des Dialogfelds [Assistent für die Konfiguration des Verwaltungs-Data Warehouses](#Wizard) enthalten. Weitere Informationen zum Konfigurieren eines Datensammlers finden Sie unter [Configure Properties of a Data Collector](../../relational-databases/data-collection/configure-properties-of-a-data-collector.md).  
  
> [!NOTE]  
>  Wenn der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent für die Verwendung eines der Systemdienstkonten (Lokales System, Netzwerkdienst oder Lokaler Dienst) konfiguriert ist und das Verwaltungs-Data Warehouse auf einer anderen Instanz als der Datensammler erstellt wird, müssen Sie die Sammlungssätze so konfigurieren, dass sie einen Proxy zum Hochladen von Daten in das Verwaltungs-Data Warehouse verwenden.  
  
### Konfigurieren des Verwaltungs-Data Warehouses auf einer einzelnen oder mehreren [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Stellen Sie sicher, dass der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent ausgeführt wird.  
  
2.  Erweitern Sie im Objekt-Explorer den Knoten **Verwaltung** .  
  
3.  Klicken Sie mit der rechten Maustaste auf **Datensammlung**, erweitern Sie **Aufgaben**, und klicken Sie dann auf **Verwaltungs-Data Warehouse konfigurieren**.  
  
4.  Verwenden Sie den [Assistenten für die Konfiguration des Verwaltungs-Data Warehouses](#Wizard) , um ein Verwaltungs-Data Warehouse zu erstellen, die Anmeldungen zu konfigurieren, die Datensammlung zu aktivieren und die **Systemdaten-Sammlungssätze**zu starten.  
  
     Zum Konfigurieren mehrerer Instanzen fahren Sie mit Schritt 5 fort.  
  
    > [!NOTE]  
    >  Es wird empfohlen, für Bereitstellungen, bei denen der Datensammler auf mehreren Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installiert ist, die dasselbe Verwaltungs-Data Warehouse verwenden, Proxys zu verwenden.  
  
5.  Öffnen Sie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] auf einer anderen Instanz, und führen Sie eine der folgenden Aktionen aus:  
  
    -   Verwenden Sie den Assistenten für die Konfiguration des Verwaltungs-Data Warehouses, um die Datensammlung für das vorhandene Verwaltungs-Data Warehouse zu konfigurieren.  
  
    -   Klicken Sie mit der rechten Maustaste auf **Datensammlung** und dann auf **Eigenschaften**. Geben Sie auf der Registerkarte **Allgemein** das vorhandene Verwaltungs-Data Warehouse und den Server an, auf dem es installiert ist.  
  
6.  Wiederholen Sie Schritt 5, bis alle Datenbankinstanzen, die den Datensammler verwenden, so konfiguriert sind, dass sie Daten in das gemeinsam verwendete Verwaltungs-Data Warehouse hochladen.  
  
####  <a name="Wizard"></a> Assistent für die Konfiguration des Verwaltungs-Data Warehouses  
 **Willkommensseite**  
  
 Die Willkommensseite ist die Anfangsseite des Assistenten für die Konfiguration der Datensammlung. Die Anzeige dieser Seite ist optional.  
  
 **Diese Anfangsseite nicht mehr anzeigen.**  
 Wählen Sie diese Option aus, damit diese Seite beim nächsten Start des Assistenten für die Konfiguration der Datensammlung nicht mehr angezeigt wird.  
  
 **Konfiguration der Verwaltungs-Data Warehouse-Speicherseite**  
  
 Auf dieser Seite können Sie einen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenbankserver und ein Verwaltungs-Data Warehouse auswählen. Das Verwaltungs-Data Warehouse ist eine relationale Datenbank, in der aufgelistete Daten gespeichert werden.  
  
> [!NOTE]  
>  Sie müssen die erforderlichen Berechtigungen zum Erstellen des Verwaltungs-Data Warehouses auf dem Server besitzen. Weitere Informationen finden Sie unter [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md). Zudem müssen Sie die erforderlichen Berechtigungen zum Erstellen von Anmeldenamen für Verwaltungs-Data Warehouse-Rollen besitzen.  
  
 **Servername**  
 Gibt den Namen des Servers an, der als Host für das Verwaltungs-Data Warehouse fungiert.  
  
 Bei der Konfiguration eines Verwaltungs-Data Warehouse ist **Servername** stets der Name des lokalen Servers und kann nicht geändert werden.  
  
 **Datenbankname**  
 Gibt die relationale Datenbank an, in der aufgelistete Daten gespeichert werden. Wählen Sie eine vorhandene Datenbank aus der Liste aus, oder klicken Sie auf **Neu** , um im Dialogfeld **Neue Datenbank** eine neue Datenbank zu erstellen.  
  
 Die Option **Neu** ist nur beim Konfigurieren eines Datensammlungssatzes verfügbar.  
  
 **Zuordnen von Anmeldenamen und Benutzern (Seite)**  
  
 Verwenden Sie diese Seite, um Benutzerrollen für Datenbanken Anmeldenamen für das Verwaltungs-Data Warehouse zuzuordnen.  
  
 **Benutzer, die dieser Anmeldung zugeordnet sind**  
 Zeigt die Anmeldungen an, die auf dem Server vorhanden sind, der als Host für das Verwaltungs-Data Warehouse fungiert. Jede Zeile enthält folgende Elemente, die bearbeitet werden können: das Kontrollkästchen **Zuordnen** , einen Namen für die **Anmeldung** und einen **Typ** für die Anmeldung.  
  
 Geben Sie eine Anmeldung durch Aktivieren des Kontrollkästchens **Zuordnen** für die Anmeldung an.  
  
 **Mitgliedschaft in Datenbankrolle für:** *\<Data Warehouse-Name>*  
 Wählen Sie die Verwaltungs-Data Warehouse-Rolle aus, der der Anmeldenamen zugeordnet ist. Aktivieren Sie zu diesem Zweck das bzw. die entsprechenden Kontrollkästchen:  
  
-   **mdw_admin**  
  
-   **mdw_reader**  
  
-   **mdw_writer**  
  
 **Neue Anmeldung**  
 Öffnen Sie das Dialogfeld **Anmeldung – Neu**, und erstellen Sie eine neue Anmeldung für das Verwaltungs-Data Warehouse.  
  
 **Seite "Assistenten abschließen"**  
  
 Auf dieser Seite können Sie die Datensammlungskonfiguration überprüfen und abschließen. Der im Ansichtsfenster angezeigten Struktur ist zu entnehmen, welche Konfigurationen angewendet und welche Aktionen ausgeführt werden, wenn Sie auf **Fertig stellen**klicken.  
  
 **Konfigurieren des Fortschritts des Assistenten für die Konfiguration der Datensammlung (Seite)**  
  
 Auf dieser Seite können Sie die Ergebnisse der einzelnen Konfigurationsschritte anzeigen.  
  
 **Details**  
 Zeigt jeden Konfigurationsschritt als Zeile im Raster **Details** an. In jeder Zeile wird in der Spalte **Aktion** der Schritt beschrieben, und in der Spalte **Status** wird angegeben, ob der Schritt erfolgreich ausgeführt wurde oder fehlgeschlagen ist. Wenn ein Fehler aufgetreten ist, wird in der Spalte **Meldung** eine Meldung angezeigt.  
  
 **Beenden**  
 Beendet die Verarbeitung des Assistenten.  
  
 **Bericht**  
 Zeigt einen Bericht über die Datensammlungskonfiguration an. Die folgenden Berichtsoptionen stehen zur Verfügung:  
  
-   Bericht anzeigen  
  
-   Bericht in Datei speichern  
  
-   Bericht in Zwischenablage kopieren  
  
-   Bericht als E-Mail senden  
  
 **Schließen**  
 Schließen Sie den Assistenten.  
  
## Siehe auch  
 [sp_syscollector_enable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)   
 [sp_syscollector_disable_collector &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)   
 [Verwalten von Datensammlungen](../../relational-databases/data-collection/manage-data-collection.md)  
  
  