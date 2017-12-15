---
title: Filter generieren | Microsoft-Dokumentation
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
f1_keywords: sql13.rep.newpubwizard.generatefilters.f1
ms.assetid: be28515c-5d6d-467b-b933-d7c8d97a45b4
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3e86760f99dd98a405ec4e0efcdf0516485a09b
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="generate-filters"></a>Filter generieren
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe des Dialogfelds **Filter generieren** können Sie einen Zeilenfilter für eine Tabelle in einer Mergeveröffentlichung definieren. Die Replikation erweitert dann den Filter automatisch auf andere Tabellen, die durch Fremdschlüsselbeziehungen verbunden sind. Wenn Sie z. B. einen Filter für eine Kundentabelle so definieren, dass diese nur Daten zu französischen Kunden enthält, dann erweitert die Replikation den Filter derart, dass verknüpfte Tabellen mit Bestellungen und Bestellungsdetails nur Informationen enthalten, die sich auf französische Kunden beziehen.  
  
## <a name="options"></a>Optionen  
 Dieses Dialogfeld enthält einen dreistufigen Vorgang zum Erstellen eines Zeilenfilters für eine Tabelle. Der Filter wird dann auf die Tabellen erweitert, die mit der gefilterten Tabelle über Primärschlüssel- und Fremdschlüsselbeziehungen verknüpft sind. Wenn z. B. drei Tabellen gegeben sind, **Customer**, **SalesOrderHeader**und **SalesOrderDetail**, mit einer Beziehung zwischen **Customer** und **SalesOrderHeader**sowie einer Beziehung zwischen **SalesOrderHeader** und **SalesOrderDetail**, dann können Sie einen Zeilenfilter auf **Customer**anwenden, und die Replikation erweitert diesen Filter auf **SalesOrderHeader** und **SalesOrderDetail**.  
  
1.  **Wählen Sie die zu filternde Tabelle aus.**  
  
     Wählen Sie eine Tabelle aus dem Dropdownlistenfeld aus. Tabellen werden im Listenfeld nur dann angezeigt, wenn sie auf der Seite **Artikel** ausgewählt wurden.  
  
2.  **Vervollständigen Sie die Filteranweisung, um die von Abonnenten empfangenen Tabellenzeilen zu identifizieren.**  
  
     Definieren Sie eine neue Filteranweisung. Im Listenfeld **Spalten** werden alle Spalten aufgeführt, die Sie aus einer in **Wählen Sie die zu filternde Tabelle aus**ausgewählten Tabelle veröffentlichen. Der Textbereich **Filteranweisung** enthält den Standardtext im folgenden Format:  
  
     `SELECT <published_columns> FROM [tableowner].[tablename] WHERE`  
  
     Der Text kann nicht geändert werden. Geben Sie die Filterklausel nach dem WHERE-Schlüsselwort mithilfe der standardmäßigen [!INCLUDE[tsql](../../includes/tsql-md.md)] -Syntax ein.  
  
    > [!IMPORTANT]  
    >  Aus Leistungsgründen ist es empfehlenswert, keine Funktionen auf Spaltennamen in Klauseln für parametrisierte Zeilenfilter anzuwenden, wie z. B. `LEFT([MyColumn]) = SUSER_SNAME()`. Wenn Sie HOST_NAME in einer Filterklausel verwenden und den HOST_NAME-Wert überschreiben, müssen Datentypen eventuell mit CONVERT konvertiert werden. Weitere Informationen zu bewährten Methoden für diesen Fall finden Sie im Abschnitt über das Überschreiben des HOST_NAME()-Werts im Thema [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  **Geben Sie an, wie viele Abonnements Daten aus dieser Tabelle empfangen.**  
  
     Nur in[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] und höheren Versionen. Mithilfe von Mergereplikationen können Sie den für Ihre Daten und Ihre Anwendung am besten geeigneten Partitionstyp angeben. Wenn Sie **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**auswählen, legt die Mergereplikation die Option für nicht überlappende Partitionen fest. Nicht überlappende Partitionen arbeiten zur Leistungsverbesserung mit vorausberechneten Partitionen zusammen, wobei nicht überlappende Partitionen die bei vorausberechneten Partitionen entstehenden Uploadkosten minimieren. Die Leistungsvorteile nicht überlappender Partitionen treten deutlicher hervor, wenn die verwendeten parametrisierten Filter und Joinfilter komplexer sind. Bei Auswahl dieser Option müssen Sie jedoch sicherstellen, dass die Daten so partitioniert werden, dass eine Zeile nicht für mehrere Abonnenten repliziert werden kann. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
 Nachdem Sie einen Filter hinzugefügt haben, klicken Sie auf **OK** , um das Dialogfeld zu schließen. Der von Ihnen angegebene Filter wird analysiert und für die Tabelle in der SELECT-Klausel ausgeführt. Wenn die Filteranweisung Syntaxfehler oder andere Probleme enthält, werden Sie benachrichtigt und können die Filteranweisung bearbeiten.  
  
 Nachdem die Anweisung analysiert ist, erstellt die Replikation die erforderlichen Joinfilter. Wenn Sie bis jetzt für den Verleger, für den der Assistent ausgeführt wird, den Verteiler nicht konfiguriert haben, werden Sie jetzt aufgefordert, ihn zu konfigurieren.  
  
## <a name="see-also"></a>Siehe auch  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [Filtern von veröffentlichten Daten](../../relational-databases/replication/publish/filter-published-data.md)   
 [Verknüpfungsfilter](../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)   
 [Veröffentlichen von Daten und Datenbankobjekten](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
