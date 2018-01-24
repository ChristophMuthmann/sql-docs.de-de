---
title: Automatisches Generieren einer Reihe von Joinfiltern zwischen Mergeartikeln | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic join filter generation
- join filters
ms.assetid: 7ef419f4-c17f-42a5-9068-174a3ec08941
caps.latest.revision: "38"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ad22d47f8673b81ce7cc8c8f2bda399f59f9b96
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="automatically-generate-join-filters-between-merge-articles"></a>Automatisches Generieren einer Reihe von Joinfiltern zwischen Mergeartikeln
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Mithilfe des Assistenten für neue Veröffentlichung auf der Seite **Tabellenzeilen filtern** oder des Dialogfelds **Veröffentlichungseigenschaften – \<Veröffentlichung>** auf der Seite **Zeilen filtern** können Sie eine Reihe von Joinfiltern automatisch generieren. Weitere Informationen zum Verwenden des Assistenten sowie Zugriff auf das Dialogfeld finden Sie unter [Erstellen einer Veröffentlichung](../../../relational-databases/replication/publish/create-a-publication.md) und [Anzeigen und Ändern von Veröffentlichungseigenschaften](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
> [!NOTE]  
>  Wenn Sie nach dem Initialisieren von Abonnements für die Veröffentlichung automatisch eine Reihe von Joinfiltern im Dialogfeld **Veröffentlichungseigenschaften - \<Veröffentlichung>** generieren, müssen Sie eine neue Momentaufnahme generieren und nach der Änderung alle Abonnements erneut initialisieren. Weitere Informationen zum Ändern von Eigenschaften finden Sie unter [Ändern von Veröffentlichungs- und Artikeleigenschaften](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
 Joinfilter können manuell für eine Gruppe von Tabellen erstellt werden. Die Filter können auch automatisch durch die Replikation anhand der Primärschlüssel/Fremdschlüssel-Beziehungen generiert werden, die für die Tabellen definiert sind. Weitere Informationen zum manuellen Definieren von Joinfiltern finden Sie unter [Definieren und Ändern eines Verknüpfungsfilters zwischen Mergeartikeln](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
### <a name="to-automatically-generate-a-set-of-join-filters-between-merge-articles"></a>So generieren Sie automatisch eine Reihe von Joinfiltern zwischen Mergeartikeln  
  
1.  Klicken Sie im Assistenten für neue Veröffentlichung auf der Seite **Tabellenzeilen filtern** oder im Dialogfeld **Veröffentlichungseigenschaften -** Veröffentlichung> **auf der Seite \<Zeilen filtern** auf **Hinzufügen**, und klicken Sie dann auf **Filter automatisch generieren**.  
  
    > [!NOTE]  
    >  Beim automatischen Generieren von Filtern werden alle vorhandenen Zeilenfilter oder Joinfilter in der Veröffentlichung gelöscht. Sie können nach dem automatischen Generieren einer Reihe von Filtern weitere Filter hinzufügen.  
  
2.  Folgen Sie zum Erstellen eines Zeilenfilters dem Verfahren im Dialogfeld **Filter generieren** . Der Zeilenfilter wird dann basierend auf den aufgeführt automatisch auf die Tabellen ausgeweitet, die mit der gefilterten Tabelle verbunden sind.  
  
    1.  Wählen Sie im Dropdown-Listenfeld eine Tabelle aus, die Sie filtern möchten.  
  
    2.  Erstellen Sie im Textfeld **Filteranweisung** eine Filteranweisung. Sie können den Text direkt in den Textbereich eingeben, und Sie können Spalten auch mit Drag und Drop aus dem Listenfeld **Spalten** einfügen.  
  
         Der Textbereich **Filteranweisung** enthält den Standardtext im folgenden Format:  
  
        ```  
        SELECT <published_columns> FROM [tableowner].[tablename] WHERE  
        ```  
  
         Der Standardtext kann nicht geändert werden. Geben Sie die Filterklausel für einen statischen Zeilenfilter oder einen parametrisierten Zeilenfilter nach dem WHERE-Schlüsselwort mithilfe der standardmäßigen SQL-Syntax ein. Die vollständige Filterklausel für einen parametrisierten Zeilenfilter würde wie folgt aussehen:  
  
        ```  
        SELECT <published_columns> FROM [HumanResources].[Employee] WHERE LoginID = SUSER_SNAME()  
        ```  
  
         Verwenden Sie einen zweiteiligen Namen für die WHERE-Klausel, drei- oder vierteilige Namen werden nicht unterstützt.  
  
    3.  Geben Sie Filteroptionen an.  
  
         Wählen Sie die Option, die dem Verfahren entspricht, mit dem Daten an Abonnenten weitergegeben werden: **Eine Zeile aus dieser Tabelle wird an mehrere Abonnements gesendet** oder **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**. Wenn Sie **Eine Zeile aus dieser Tabelle wird nur an ein Abonnement gesendet**auswählen, kann die Mergereplikation die Leistung optimieren, da weniger Metadaten gespeichert und verarbeitet werden. Sie müssen jedoch sicherstellen, dass die Daten so partitioniert werden, dass eine Zeile nicht für mehrere Abonnenten repliziert werden kann. Weitere Informationen finden Sie im Abschnitt zum Festlegen von Partitionsoptionen unter [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     Der von Ihnen angegebene Filter wird analysiert und für die Tabelle in der SELECT-Klausel ausgeführt. Wenn die Filteranweisung Syntaxfehler oder andere Probleme enthält, werden Sie benachrichtigt und können die Filteranweisung bearbeiten.  
  
     Nach der Analyse der Anweisung erstellt die Replikation die nötigen Joinfilter und zeigt sie auf der Seite **Tabellenzeilen filtern** oder der Seite **Zeilen filtern** im Bereich **Gefilterte Tabellen** an. Wenn Sie Filter im Assistenten für neue Veröffentlichung generieren und noch nicht den Verteiler für den Verleger konfiguriert haben, für den dieser Assistent ausgeführt wird, werden Sie zum Konfigurieren des Verteilers aufgefordert.  
  
4.  Wenn Sie sich im Dialogfeld **Veröffentlichungseigenschaften.-.\<Veröffentlichung>** befinden, klicken Sie auf **OK**, um zu speichern und das Dialogfeld zu schließen.  
  
### <a name="to-modify-a-filter-that-was-automatically-generated"></a>So ändern Sie einen automatisch generierten Filter  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Tabellenzeilen filtern** oder im Dialogfeld **Veröffentlichungseigenschaften –** Veröffentlichung> **auf der Seite \<Zeilen filtern** im Bereich **Gefilterte Tabellen** einen Filter aus, und klicken Sie dann auf **Bearbeiten**.  
  
2.  Ändern Sie den Filter im Dialogfeld **Filter bearbeiten** oder **Join bearbeiten** .  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-filter-that-was-automatically-generated"></a>So löschen Sie einen automatisch generierten Filter  
  
1.  Wählen Sie im Assistenten für neue Veröffentlichung auf der Seite **Tabellenzeilen filtern** oder im Dialogfeld **Veröffentlichungseigenschaften –** Veröffentlichung> **auf der Seite \<Zeilen filtern** im Bereich **Gefilterte Tabellen** einen Filter aus, und klicken Sie dann auf **Löschen**.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
