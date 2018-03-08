---
title: Tabellenzeilen filtern | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.newpubwizard.filtertablerows.f1
ms.assetid: 005f5c71-0401-490e-8823-adc54a2e9675
caps.latest.revision: "25"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7917c67c302800a23ed20c974115641f644b513f
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="filter-table-rows"></a>Tabellenzeilen filtern
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe der Seite **Tabellenzeilen filtern** können Sie:  
  
-   Statische Zeilenfilter auf Tabellenartikel in Momentaufnahme-, Transaktions- und Mergeveröffentlichungen anwenden  
  
-   Parametrisierte Zeilenfilter auf Tabellenartikel in Mergeveröffentlichungen anwenden  
  
-   Joinfilter verwenden, um Filter für Mergetabellenartikel auf verwandte Tabellenartikel zu erweitern  
  
 Weitere Informationen zu Filteroptionen finden Sie unter [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md). Die Filterung kann auf der Seite **Zeilen filtern** im Dialogfeld **Veröffentlichungseigenschaften** geändert werden.  
  
 Wenn Sie die optimale Leistung Ihrer Anwendung sicherstellen und den am Remotestandort benötigten Speicherplatz verringern möchten, oder wenn Sie die Verfügbarkeit bestimmter Daten für bestimmte Abonnenten beschränken möchten, sollten Sie nur die erforderlichen Daten veröffentlichen. Die Veröffentlichung kann sowohl ungefilterte als auch gefilterte Tabellen einschließen. Beispielsweise könnten Sie die vollständige (ungefilterte) Tabelle der Firmenprodukte einschließen und Zeilenfilter verwenden, um eine gefilterte Tabelle der Kunden aus einer bestimmten Region anzugeben. Das Filtern von veröffentlichten Daten bietet folgende Möglichkeiten:  
  
-   Minimieren der über das Netzwerk gesendeten Datenmenge.  
  
-   Reduzieren des erforderlichen Speicherplatzes beim Abonnenten.  
  
-   Anpassen von Veröffentlichungen und Anwendungen an die individuellen Anforderungen des Abonnenten.  
  
-   Vermeiden oder Reduzieren von Konflikten beim Aktualisieren von Daten durch Abonnenten, da unterschiedliche Datenpartitionen an verschiedene Abonnenten gesendet werden können (es ist nicht möglich, dass mehrere Abonnenten dieselben Datenwerte aktualisieren).  
  
-   Vermeiden der Übertragung vertraulicher Daten. Mithilfe von Zeilenfiltern und Spaltenfiltern kann der Datenzugriff für Abonnenten eingeschränkt werden. Im Fall von Mergereplikationen gelten besondere Sicherheitsüberlegungen, wenn Sie einen parametrisierten Filter verwenden, der HOST_NAME() einschließt. Weitere Informationen finden Sie im Abschnitt über das Filtern mit HOST_NAME() unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Ein Filter muss die von der Replikation verwendete **rowguidcol** nicht einschließen, um Zeilen zu identifizieren. Standardmäßig ist dies die Spalte, die zum Zeitpunkt hinzugefügt wurde, als Sie die Mergereplikation eingerichtet haben, und sie heißt **rowguid**.  
  
## <a name="options"></a>Tastatur  
 **Gefilterte Tabellen**  
 Dieser Bereich wird mit Filtern aufgefüllt, während Sie den Tabellenartikeln in der Veröffentlichung Filter hinzufügen. Tabellen mit Zeilenfiltern werden im Bereich als Knoten der obersten Ebene angezeigt. Für Mergeveröffentlichungen werden Tabellen, auf die das Filtern durch einen Joinfilter erweitert wurde, als untergeordnete Knoten angezeigt.  
  
 **Hinzufügen**  
 Klicken Sie auf **Hinzufügen** , um ein Dialogfeld aufzurufen, mit dem Sie Tabellenartikel filtern können. Wenn Sie für eine Momentaufnahme- oder Transaktionsveröffentlichung auf **Hinzufügen** klicken, wird sofort ein Dialogfeld geöffnet. Wenn Sie für eine Mergeveröffentlichung auf **Hinzufügen** klicken, werden drei Auswahlmöglichkeiten angezeigt: **Filter hinzufügen**; **Join hinzufügen, um den ausgewählten Filter zu erweitern**; **Filter automatisch generieren**.  
  
-   Wählen Sie **Filter hinzufügen** aus, um das Dialogfeld **Filter hinzufügen** aufzurufen. Mithilfe dieses Dialogfelds können Sie Zeilenfilter auf einen Tabellenartikel anwenden. Im Dialogfeld **Filter hinzufügen** können Sie beispielsweise angeben, dass eine Tabelle mit Kundendaten nur Daten von französischen Kunden enthalten soll, wenn eine Replikation an Abonnenten erfolgt.  
  
-   Wählen Sie **Join hinzufügen, um den ausgewählten Filter zu erweitern** , um das Dialogfeld **Join hinzufügen** aufzurufen. Mithilfe des Dialogfelds **Join hinzufügen** können Sie einen Zeilenfilter so erweitern, dass Daten in Tabellen gefiltert werden, die mit der den Zeilenfilter enthaltenden Tabelle verbunden sind. Wenn beispielsweise eine Kundentabelle so gefiltert wird, dass sie nur Daten zu französischen Kunden enthält und eine verbundene Tabelle für Kundenbestellungen vorhanden ist, können Sie einen Join dieser beiden Tabellen definieren, damit die Bestelltabelle nur Bestellungen von französischen Kunden enthält.  
  
    > [!NOTE]  
    >  Diese Option ist nur verfügbar, wenn Sie im Filterbereich zunächst die Basistabelle des Joins ausgewählt haben.  
  
-   Wählen Sie **Filter automatisch generieren** aus, um das Dialogfeld **Filter generieren** aufzurufen. Mithilfe dieses Dialogfelds können Sie einen Zeilenfilter für eine Tabelle in einer Mergeveröffentlichung definieren, durch die die Replikation automatisch auf andere Tabellen erweitert wird, die durch Fremdschlüsselbeziehungen verbunden sind. Eine Veröffentlichung könnte beispielsweise drei Tabellen enthalten: eine Kundentabelle, eine Bestelltabelle (mit einem Fremdschlüssel zur Kundentabelle) und eine Tabelle mit den Bestellungsdetails (mit einem Fremdschlüssel zur Bestelltabelle). Wenn Sie einen Zeilenfilter für die Kundentabelle definieren, wird die Replikation auf die anderen Tabellen erweitert.  
  
    > [!NOTE]  
    >  Werden Filter durch die Replikation automatisch generiert, werden für die Veröffentlichung vorhandene Filter gelöscht. Wenn Sie sowohl automatisch generierte wie auch manuell angegebene Filter einschließen möchten, müssen Sie zunächst Filter generieren. Sie können für jede Veröffentlichung nur einen Satz automatisch generierter Filter angeben.  
  
 **Bearbeiten**  
 Wählen Sie im Filterbereich einen Zeilenfilter oder einen Joinfilter aus, und klicken Sie auf **Bearbeiten** , um das Dialogfeld **Filter bearbeiten** oder **Join bearbeiten** aufzurufen.  
  
 **Delete**  
 Wählen Sie im Filterbereich einen Zeilenfilter oder einen Joinfilter aus, und klicken Sie auf **Löschen** , um den Filter zu löschen.  
  
 **Tabelle suchen**  
 Ist nur für Mergeveröffentlichungen mit Joinfiltern verwendbar. Klicken Sie auf **Tabelle suchen** , um eine Tabelle in einer komplexen Filterstruktur zu suchen. In einer Datenbank mit komplexen Beziehungen kann eine Tabelle mit mehreren Tabellen verknüpft sein. Deshalb kann sie in der Filterstruktur mehrmals angezeigt werden.  
  
 Die eigentliche Tabelle wird in der Struktur nur einmal angezeigt. An den übrigen Stellen wird die Tabelle durch eine Verknüpfung dargestellt. Bei einer Verknüpfung mit einer Tabelle handelt es sich nur um einen Verweis auf die Tabelle. Es werden keine untergeordneten Knoten der Tabelle angezeigt. Ein Verknüpfungsknoten ist mit einem Verknüpfungspfeil markiert. Wenn Sie den Knoten erweitern, wird der Text **Klicken Sie auf „Tabelle suchen“, um die Tabelle für \<Tabellenname> anzuzeigen** angezeigt.  
  
 Wählen Sie im Bereich einen Verknüpfungsknoten aus, und klicken Sie auf **Tabelle suchen**. Der Bereich wird erweitert, und die Tabelle wird hervorgehoben. Wenn Sie auf **Tabelle suchen** klicken, ohne dass ein Verknüpfungsknoten ausgewählt wurde, wird ein Dialogfeld **Tabelle suchen** aufgerufen.  
  
 **Filter**  
 Enthält die [!INCLUDE[tsql](../../includes/tsql-md.md)] -Definition für die im Filterbereich ausgewählten Filter.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
