---
title: Verwenden des Volltextindizierungs-Assistenten | Microsoft-Dokumentation
ms.custom: 
ms.date: 08/19/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: search
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.fulltextindexingwizard.welcome.f1
- sql13.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql13.swb.fulltextindexingwizard.progress.f1
- sql13.swb.fulltextindexingwizard.selectchangetracking.f1
- sql13.swb.fulltextindexingwizard.selectacatalog.f1
- sql13.swb.fulltextindexingwizard.selectatableorview.f1
- sql13.swb.fulltextindexingwizard.selectanindex.f1
- sql13.swb.fulltextindexingwizard.summary.f1
- sql13.swb.fulltextindexingwizard.selecttablecolumns.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
caps.latest.revision: "24"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4cfca84ed59bd6922a6667a0b214668836e421ba
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-full-text-indexing-wizard"></a>Verwenden des Volltextindizierungs-Assistenten
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] Der Volltextindizierungs-Assistent in SSMS führt Sie durch eine Reihe von Arbeitsschritten, die Ihnen das Erstellen eines Volltextindexes erleichtern.  
  
## <a name="create-a--full-text-index"></a>Erstellen eines Volltextindexes 

1. Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf die Tabelle, für die Sie einen Volltextindex erstellen möchten, zeigen Sie auf **Volltextindex**, und klicken Sie anschließend auf **Volltextindex definieren**. Diese Aktion startet den Assistenten in einem separaten Fenster.
   Klicken Sie auf „Weiter“. 
  
2. **Eindeutiger Index**  Wählen Sie einen Index aus der Dropdownliste aus. Der Index muss genau eine Schlüsselspalte haben, muss eindeutig sein und darf keine NULL-Werte zulassen. Wählen Sie als eindeutigen Volltextschlüssel stets den kleinsten eindeutigen Index aus. Für die bestmögliche Leistung ist ein gruppierter Index zu empfehlen.  
  
3.  **Verfügbare Spalten** Aktivieren Sie das Kontrollkästchen neben allen Spaltennamen für Spalten, die Sie einschließen möchten.  Kontrollkästchen neben dem Spaltennamen. Unzulässige Spalten werden abgeblendet dargestellt und ihre Kontrollkästchen sind deaktiviert.  
  
4. **Sprache für die Wörtertrennung** Wählen Sie eine Sprache aus der Dropdownliste aus. Diese Auswahl wird verwendet, um die richtigen Wörtertrennungen für den Index zu identifizieren. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] In werden mithilfe von Wörtertrennzeichen Wortgrenzen in den volltextindizierten Daten gekennzeichnet.  
  
5.  **Typspalte** Wählen Sie den Namen der Spalte aus, in der der Dokumenttyp der volltextindizierten Spalte enthalten ist.  
> **HINWEIS:** Das Feld  **Typspalte** ist nur verfügbar, wenn die unter **Verfügbare Spalten** genannte Spalte vom Typ **varbinary(max)** oder **image**ist.  
  
6. **Statistische Semantik** Wählen Sie aus, ob die semantische Indizierung für die ausgewählte Spalte aktiviert werden soll. Weitere Informationen finden Sie unter [Semantische Suche &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
>**HINWEISE** 
>
>Wenn die von Ihnen gewählte Sprache nicht über ein zugeordnetes semantisches Sprachmodell verfügt, dann ist das Kontrollkästchen **Statistische Semantik** nicht aktiviert. Wenn Sie **Statistische Semantik** vor einer **Sprache**auswählen, werden im Dropdown-Kombinationsfeld nur die Sprachen angezeigt, für die das semantische Sprachmodell unterstützt wird.  
>
> Die semantische Suche ist für die **Azure SQL-Datenbank nicht verfügbar**. Die Option „Statistische Semantik“ wird nicht angezeigt, wenn dieser Assistent für eine Azure SQL-Datenbank ausgeführt wird.
  
7. Aktivieren Sie die Optionen zur Änderungsnachverfolgung.  
  
     **Automatisch**  
     Wählen Sie diese Optionsschaltfläche, wenn der Volltextindex im Falle von Änderungen an den zugrunde liegenden Daten automatisch aktualisiert werden soll.  
  
     **Manuell**  
     Wählen Sie diese Optionsschaltfläche, wenn der Volltextindex im Falle von Änderungen an den zugrunde liegenden Daten nicht automatisch aktualisiert werden soll. Die Änderungen an den zugrunde liegenden Daten bleiben erhalten. Um jedoch die Änderungen im Volltextindex zu berücksichtigen, müssen Sie diesen Prozess manuell oder über einen Zeitplan starten.  
  
     **Änderungen nicht nachverfolgen**  
     Wählen Sie diese Optionsschaltfläche, wenn der Volltextindex bei Änderungen an den zugrunde liegenden Daten nicht aktualisiert werden soll.  
  
8.  Starten Sie die vollständige Auffüllung, wenn der Index erstellt wird (nur verfügbar, wenn Sie keine Änderungen überwachen).
  
     Wählen Sie diese Optionsschaltfläche, um nach erfolgreichem Abschluss dieses Assistenten eine vollständige Auffüllung zu starten. Dabei wird die Volltext-Indexstruktur im Katalog erstellt und der Katalog mit volltextindizierten Daten aufgefüllt.  
     
     Klicken Sie auf „Weiter“.
  
## <a name="catalog-index-filegroup-and-stoplist"></a>Katalog, Indexdateigruppe und Stoppliste   
  
9.  **Volltextkatalog auswählen**  

     **Katalog auswählen:** Wählen Sie einen Volltextkatalog aus der Liste aus. Der Standardkatalog für die Datenbank entspricht standardmäßig dem in der Liste ausgewählten Element. Wenn keine Kataloge verfügbar sind, wird die Liste deaktiviert, und das Kontrollkästchen **Neuen Katalog erstellen** wird überprüft und deaktiviert.  
  
  oder
  
 10. **Neuen Katalog erstellen**
 - Volltextkatalog auswählen  
  
    a. **Name**  
     Geben Sie einen Namen für Ihren neuen Volltextkatalog ein.  
  
     b. **Als Standardkatalog festlegen**  
     Wählen Sie diese Option aus, um diesen Katalog als Standardkatalog für die Datenbank festzulegen.  
  
     c. **Unterscheidung nach Akzent**  
     Geben Sie an, ob für den neuen Katalog nach Akzenten unterschieden wird. Wenn in der Datenbank nach Akzent unterschieden wird, ist die Option **Mit Unterscheidung** standardmäßig aktiviert.  
  
     d. **Indexdateigruppe auswählen**  
     Geben Sie die Dateigruppe an, für die der Volltextindex erstellt werden soll.  
  
     e. Wählen Sie einen Wert:  
      |Wert|Beschreibung|  
      |-----------|-----------------|
      |**<default>**| Wenn die Tabelle oder Sicht nicht partitioniert ist, wählen Sie diese Option, um dieselbe Dateigruppe wie die zugrunde liegende Tabelle oder Sicht zu verwenden. Wenn die Tabelle oder Sicht partitioniert ist, wird die primäre Dateigruppe verwendet.|
      |**PRIMARY**|Wählen Sie diese Option, um die primäre Dateigruppe für den neuen Volltextindex zu verwenden.|
      *Eine vom Benutzer angegebene Standarddateigruppe*|Wenn eine benutzerdefinierte Standardstoppliste vorhanden ist, wählen Sie den Namen in der Liste aus, um die zugehörige Dateigruppe für den neuen Volltextindex zu verwenden.|   
  
     
 11. **Volltext-Stoppliste auswählen**  
     Geben Sie eine Stoppliste an, die für den Volltextindex verwendet werden soll, oder deaktivieren Sie die Stopplistenverwendung.  
  
     Stoppwörter werden über Objekte mit dem Namen "Stoplisten" in Datenbanken verwaltet. Eine *Stoppliste* ist eine Liste mit Stoppwörtern, die, wenn sie einem Volltextindex zugeordnet ist, auf Volltextabfragen für diesen Index angewendet wird. Weitere Informationen finden sie unter [Konfigurieren und Verwalten von Stoppwörtern und Stopplisten für Volltextsuche](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Folgende Werte sind möglich:  
  
   |Wert|Beschreibung|  
    |-----------|-----------------|  
    |**<system>**|Wählen Sie diese Option, um die Systemstoppliste für den neuen Volltextindex zu verwenden. Dies ist die Standardeinstellung.|  
    |**<off>**|Wählen Sie diese Option, um Stopplisten für den neuen Volltextindex zu deaktivieren.|  
    |*user-defined-stoplist-name*|Die Liste enthält die Namen aller benutzerdefinierten Stopplisten (falls vorhanden), die für die Datenbank erstellt wurden. Wählen Sie eine beliebige benutzerdefinierte Stoppliste zur Verwendung für den neuen Volltextindex aus.|  
  
  Klicken Sie auf „Weiter“.
  
11. Optional können Sie (nur für SQL Server) auch den Auffüllungszeitplan definieren. Sofern Sie die Ausführung nicht für die Zukunft geplant haben, beginnen die Indizierungsvorgänge sofort. Die Zeitpläne werden sofort erstellt, sie werden jedoch erst zum festgelegten Zeitpunkt ausgeführt.  
  
     **Neuer Tabellenzeitplan**  
     Definieren eines Auffüllungszeitplans für eine Tabelle.  
  
     **Neuer Katalogzeitplan**  
     Definieren eines Auffüllungszeitplans für einen Volltextkatalog.  
  
     **Bearbeiten**  
     Bearbeiten eines Zeitplans.  
  
     **Delete**  
     Löschen eines Zeitplans.  
  
5.  Zeigen Sie den Status des Volltextindizierungs-Assistenten an, bzw. steuern Sie ihn.  
  
     **Beenden**  
     Unterbricht den aktuellen Vorgang und verhindert die Ausführung nachfolgender Volltextvorgänge durch den Assistenten während dieser Sitzung.  
  
     **Bericht**  
     Wenn alle Vorgänge ausgeführt wurden, können Sie auf diese Schaltfläche klicken, um auf einen Bericht zu den ausgeführten Vorgängen zuzugreifen. Sie können den Bericht anzeigen, in eine Datei drucken, in die Zwischenablage kopieren oder ihn per E-Mail versenden.  
  
  
