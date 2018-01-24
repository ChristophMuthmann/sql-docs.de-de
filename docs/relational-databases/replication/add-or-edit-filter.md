---
title: "Hinzufügen oder Bearbeiten von Filtern | Microsoft-Dokumentation"
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
f1_keywords: sql13.rep.newpubwizard.addeditfilter.f1
ms.assetid: bdd7c71d-1c59-4044-bfe8-c85f908345bb
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0461e699bbf3593f87567d3972aa7e260bca3111
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="add-or-edit-filter"></a>Hinzufügen oder Bearbeiten von Filtern
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe der Dialogfelder **Filter hinzufügen** und **Filter bearbeiten** können Sie statische Zeilenfilter und parametrisierte Zeilenfilter hinzufügen und bearbeiten.  
  
> [!NOTE]  
>  Für das Bearbeiten in einer vorhandenen Veröffentlichung ist eine neue Momentaufnahme für die Veröffentlichung erforderlich. Wenn eine Veröffentlichung Abonnements besitzt, müssen die Abonnements erneut initialisiert werden. Weitere Informationen zum Ändern von Eigenschaften finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Alle Veröffentlichungstypen können statische Filter einschließen. Mergeveröffentlichungen können auch parametrisierte Filter einschließen. Ein statischer Filter wird beim Erstellen der Veröffentlichung ausgewertet: alle Abonnenten der Veröffentlichung empfangen dieselben Daten. Ein parametrisierter Filter wird während der Replikationssynchronisierung ausgewertet: basierend auf dem Anmeldenamen oder dem Computernamen der einzelnen Abonnenten können unterschiedliche Abonnenten verschiedene Datenpartitionen empfangen. Klicken Sie im Dialogfeld auf den Link **Beispielanweisungen** , um Beispiele für die einzelnen Filtertypen anzuzeigen. Weitere Informationen zu Filteroptionen finden Sie unter [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md).  
  
 Mithilfe von Zeilenfiltern können Sie eine zu veröffentlichende Teilmenge von Zeilen aus einer Tabelle angeben. Mithilfe von Zeilenfiltern können Sie Zeilen entfernen, die Benutzern nicht angezeigt werden sollen (z. B. Zeilen mit vertraulichen oder streng vertraulichen Informationen). Mit Zeilenfiltern können Sie auch unterschiedliche Datenpartitionen erstellen, die an verschiedene Abonnenten übermittelt werden. Indem Sie unterschiedliche Datenpartitionen für verschiedene Abonnenten veröffentlichen, können Sie auch Konflikte vermeiden, die andernfalls dadurch entstehen würden, dass mehrere Abonnenten dieselben Daten aktualisieren.  
  
## <a name="options"></a>Tastatur  
 Dieses Dialogfeld umfasst einen zweistufigen Vorgang für die Transaktions- und Momentaufnahmeveröffentlichungen sowie einen dreistufigen Vorgang für Mergeveröffentlichungen. Für alle Veröffentlichungstypen ist es erforderlich, dass Sie eine zu filternde Tabelle und eine oder mehrere Spalten auswählen, die im Filter eingeschlossen sein sollen. Der Filter wird als standardmäßige WHERE-Klausel definiert.  
  
1.  **Wählen Sie die zu filternde Tabelle aus**  
  
     Wenn Sie einen bereits vorhandenen Filter bearbeiten, kann die Tabellenauswahl nicht geändert werden. Wenn Sie einen neuen Filter hinzufügen, wählen Sie aus der Dropdown-Liste eine Tabelle aus. Tabellen werden in der Liste nur angezeigt, wenn sie auf der Seite **Artikel** ausgewählt wurden und nicht bereits einen Zeilenfilter besitzen. Wenn eine Tabelle bereits einen Zeilenfilter besitzt und Sie einen neuen definieren möchten:  
  
    1.  Klicken Sie im Dialogfeld **Filter hinzufügen** auf **Abbrechen** .  
  
    2.  Wählen Sie im Filterbereich der Seite **Tabellenzeilen filtern** die Tabelle aus, und klicken Sie auf **Bearbeiten**.  
  
    3.  Bearbeiten Sie einen vorhandenen Filter im Dialogfeld **Filter bearbeiten** .  
  
2.  **Vervollständigen Sie die Filteranweisung, um die von Abonnenten empfangenen Tabellenzeilen zu identifizieren**  
  
     Definieren Sie eine neue Filteranweisung, oder bearbeiten Sie eine vorhandene. Im Listenfeld **Spalten** werden alle Spalten aufgeführt, die Sie aus einer in **Wählen Sie die zu filternde Tabelle aus**ausgewählten Tabelle veröffentlichen. Der Textbereich **Filteranweisung** enthält den Standardtext im folgenden Format:  
  
     `SELECT <published_columns> FROM [schema].[tablename] WHERE`  
  
     Der Text kann nicht geändert werden. Geben Sie die Filterklausel nach dem WHERE-Schlüsselwort mithilfe der standardmäßigen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax ein. Wenn es sich beim Verleger um einen Oracle-Verleger handelt, muss die WHERE-Klausel mit der Abfragesyntax von Oracle kompatibel sein. Verwenden Sie nach Möglichkeit komplexe Filter. Sowohl statische als auch parametrisierte Filter erhöhen die Verarbeitungszeit für Veröffentlichungen. Deshalb sollten Sie Filteranweisungen so einfach wie möglich halten.  
  
    > [!IMPORTANT]  
    >  Aus Leistungsgründen wird empfohlen, dass auf Spaltennamen in parametrisierten Zeilenfilterklauseln für Mergeveröffentlichungen keine Funktionen (z. B. `LEFT([MyColumn]) = SUSER_SNAME()`) angewendet werden. Wenn Sie HOST_NAME in einer Filterklausel verwenden und den HOST_NAME-Wert überschreiben, müssen Datentypen eventuell mit CONVERT konvertiert werden. Weitere Informationen zu bewährten Methoden für diesen Fall finden Sie im Abschnitt über das Überschreiben des HOST_NAME()-Werts im Thema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Geben Sie an, wie viele Abonnements Daten aus dieser Tabelle empfangen.**  
  
     [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höher; nur für Mergereplikationen. Mithilfe von Mergereplikationen können Sie den für Ihre Daten und Ihre Anwendung am besten geeigneten Partitionstyp angeben. Wenn Sie **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**auswählen, legt die Mergereplikation die Option für nicht überlappende Partitionen fest. Nicht überlappende Partitionen arbeiten zur Leistungsverbesserung mit vorausberechneten Partitionen zusammen, wobei nicht überlappende Partitionen die bei vorausberechneten Partitionen entstehenden Uploadkosten minimieren. Die Leistungsvorteile nicht überlappender Partitionen treten deutlicher hervor, wenn die verwendeten parametrisierten Filter und Joinfilter komplexer sind. Bei Auswahl dieser Option müssen Sie jedoch sicherstellen, dass die Daten so partitioniert werden, dass eine Zeile nicht für mehrere Abonnenten repliziert werden kann. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Nachdem Sie einen Filter hinzugefügt oder bearbeitet haben, klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld zu schließen. Der von Ihnen angegebene Filter wird analysiert und für die Tabelle in der SELECT-Klausel ausgeführt. Wenn die Filteranweisung Syntaxfehler oder andere Probleme enthält, werden Sie benachrichtigt und können die Filteranweisung bearbeiten.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
