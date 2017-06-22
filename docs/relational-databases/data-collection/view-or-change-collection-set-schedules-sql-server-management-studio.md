---
title: "Anzeigen oder Ändern von Sammlungssatz-Zeitplänen (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.dc.collectionsetprop.uploads.f1
- sql13.swb.dc.collectionsetprop.description.f1
- sql13.swb.dc.collectionsetprop.general.f1
helpviewer_keywords:
- collection sets [SQL Server], changing schedules
- schedules [SQL Server], changing collection set
- collection sets [SQL Server], viewing schedules
- schedules [SQL Server], viewing collection set
ms.assetid: 26336c98-78c5-414f-8d6a-574fc3af60c4
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b882c8e5f82beb7d467d1063695fa032ed562ca0
ms.contentlocale: de-de
ms.lasthandoff: 06/22/2017

---
# <a name="view-or-change-collection-set-schedules-sql-server-management-studio"></a>Anzeigen oder Ändern von Sammlungssatz-Zeitplänen (SQL Server Management Studio)
  Sie können Zeitpläne für den Sammlungssatz mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]anzeigen oder ändern.  
  
 Der Auflistmodus (mit oder ohne Zwischenspeicherung) bestimmt, wie Sie Änderungen an einem Zeitplan vornehmen können. Der Modus mit Zwischenspeicherung verwendet separate Zeitpläne für Sammlung und Hochladen. Der Modus ohne Zwischenspeicherung verwendet für Sammlung und Hochladen denselben Zeitplan. Die einzelnen Systemdaten-Sammlungssätze weisen den folgenden Auflistmodustyp auf:  
  
-   Die**Datenträgerverwendung** verwendet den Auflistmodus ohne Zwischenspeicherung.  
  
-   Die**Abfragestatistik** verwendet den Auflistmodus mit Zwischenspeicherung.  
  
-   Die**Serveraktivität** verwendet den Auflistmodus mit Zwischenspeicherung.  
  
### <a name="to-view-collection-set-schedules"></a>So zeigen Sie Sammlungssatz-Zeitpläne an  
  
1.  Erweitern Sie im Objekt-Explorer nacheinander die Knoten **Verwaltung** , **Datensammlung**und dann **Systemdaten-Sammlungssätze**.  
  
2.  Klicken Sie mit der rechten Maustaste auf einen Sammlungssatznamen, und klicken Sie anschließend auf **Eigenschaften** , um das Dialogfeld [Eigenschaften für Datensammlungssätze](#CollectionSet) zu öffnen.  
  
### <a name="to-change-the-schedules-for-a-cached-mode-collection-set"></a>So ändern Sie die Zeitpläne für einen Sammlungssatz im Modus mit Zwischenspeicherung  
  
1.  Erweitern Sie im Objekt-Explorer nacheinander die Knoten **Verwaltung** , **Datensammlung**und dann **Systemdaten-Sammlungssätze**.  
  
2.  Klicken Sie mit der rechten Maustaste auf einen Sammlungssatz, der den Modus mit Zwischenspeicherung verwendet, beispielsweise **Abfragestatistik**, und klicken Sie dann auf **Eigenschaften** , um das Dialogfeld [Eigenschaften für Datensammlungssätze](#CollectionSet) zu öffnen.  
  
3.  Sie können die Sammelhäufigkeit auf der Seite **Allgemein** ändern. Führen Sie hierzu folgende Schritte aus:  
  
    1.  Doppelklicken Sie im Detailbereich auf die Zahl, die in der Tabelle **Sammelelemente** für die Spalte **Sammelhäufigkeit (Sek)** angezeigt wird.  
  
    2.  Erhöhen oder verringern Sie die Sammelhäufigkeit, indem Sie eine niedrigere oder eine höhere Zahl eingeben, und drücken Sie die EINGABETASTE, um den neuen Wert zu speichern.  
  
4.  Um den vorhandenen Uploadzeitplan für den Sammlungssatz zu ändern, führen Sie die folgenden Schritte aus:  
  
    1.  Klicken Sie auf die Seite **Uploads** .  
  
    2.  Doppelklicken Sie im Detailbereich auf **Auswählen**.  
  
         Das Dialogfeld **Zeitplan für Auftrag auswählen** wird geöffnet. Die verfügbaren Zeitpläne werden als Tabelle angezeigt.  
  
    3.  Klicken Sie auf die Zeile mit dem gewünschten Zeitplan. Um beispielsweise den Zeitplan in alle 5 Minuten zu ändern, klicken Sie auf die Zeile mit dem Zeitplannamen **CollectorSchedule_Every_5min**.  
  
        > [!NOTE]  
        >  Sie können die Eigenschaften des ausgewählten Zeitplans anzeigen und bearbeiten, indem Sie auf **Eigenschaften** klicken, um das Dialogfeld **Eigenschaften des Auftragszeitplans** für diesen Zeitplan zu öffnen. In diesem Dialogfeld können Sie Zeitplaninformationen wie beispielsweise die Häufigkeit ändern.  
        >   
        >  Als Alternative zum Ändern eines vorhandenen Zeitplans können Sie einen neuen Uploadzeitplan erstellen. Klicken Sie dazu auf der Seite **Uploads** auf **Neu** . Durch diese Aktion wird das Dialogfeld **Neuer Auftragszeitplan** geöffnet, das Sie verwenden können, um einen benutzerdefinierten Zeitplan zu erstellen.  
  
    4.  Wenn Sie die Konfiguration des Zeitplans abgeschlossen haben, klicken Sie auf **OK**.  
  
         Die vorgenommenen Änderungen werden auf der Seite **Uploads** angezeigt.  
  
5.  Klicken Sie auf **OK** , um die Änderungen der Sammelhäufigkeit und des Uploadzeitplans zu speichern und um das Dialogfeld **Eigenschaften für Datensammlungssätze** zu schließen.  
  
### <a name="to-change-the-schedule-for-a-non-cached-mode-collection-set"></a>So ändern Sie den Zeitplan für einen Sammlungssatz im Modus ohne Zwischenspeicherung  
  
1.  Erweitern Sie im Objekt-Explorer nacheinander die Knoten **Verwaltung** , **Datensammlung**und dann **Systemdaten-Sammlungssätze**.  
  
2.  Klicken Sie mit der rechten Maustaste auf einen Sammlungssatz, der den Modus ohne Zwischenspeicherung verwendet, beispielsweise **Datenträgerverwendung**, und klicken Sie dann auf **Eigenschaften** , um das Dialogfeld [Eigenschaften für Datensammlungssätze](#CollectionSet) zu öffnen.  
  
     Das Dialogfeld **Eigenschaften für Datensammlungssätze** zeigt eine Ansicht im Seitenformat mit den Eigenschaften für Sammlungssätze an.  
  
3.  Klicken Sie auf **Auswählen**, um den Zeitplan für den Sammlungssatz festzulegen.  
  
     Das Dialogfeld **Zeitplan für Auftrag auswählen** wird geöffnet. Die verfügbaren Zeitpläne werden als Tabelle angezeigt.  
  
4.  Klicken Sie auf die Zeile mit dem gewünschten Zeitplan. Um beispielsweise den Zeitplan in alle 5 Minuten zu ändern, klicken Sie auf die Zeile mit dem Zeitplannamen **CollectorSchedule_Every_5min**.  
  
    > [!NOTE]  
    >  Sie können die Eigenschaften des ausgewählten Zeitplans anzeigen und bearbeiten, indem Sie auf **Eigenschaften** klicken, um das Dialogfeld **Eigenschaften des Auftragszeitplans** für diesen Zeitplan zu öffnen. In diesem Dialogfeld können Sie Zeitplaninformationen wie beispielsweise die Häufigkeit ändern.  
    >   
    >  Als Alternative zum Ändern eines vorhandenen Zeitplans können Sie einen neuen Sammlungs- und Uploadzeitplan erstellen. Klicken Sie dazu auf der Seite **Allgemein** auf **Neu** . Mit dieser Aktion wird das Dialogfeld **Neuer Auftragszeitplan** geöffnet.  
  
5.  Wenn Sie die Konfiguration des Zeitplans abgeschlossen haben, klicken Sie auf **OK**.  
  
6.  Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Eigenschaften für Datensammlungssätze** zu schließen.  
  
####  <a name="CollectionSet"></a> Eigenschaften für Datensammlungssätze (Dialogfeld)  
 **Seite Allgemein**  
  
 Auf dieser Seite können Sie konfigurieren, wie Daten aufgelistet und hochgeladen werden. Zudem können Sie Zeitpläne und Aufbewahrungsdauern für Daten im Verwaltungs-Data Warehouse konfigurieren. Darüber hinaus stehen auf dieser Seite Informationen zu Sammlungssätzen, z. B. Sammlertypen und Sammlungshäufigkeiten, sowie die für einen Sammlungssatz verwendeten Eingabeparameter zur Verfügung.  
  
 **Name**  
 Zeigt den Namen des Sammlungssatzes an, auf den diese Seite verweist.  
  
 **Datensammlung und -upload**  
 Gibt an, wie Daten aufgelistet und in das Verwaltungs-Data Warehouse hochgeladen werden. Wählen Sie eine der folgenden Optionen aus.  
  
|||  
|-|-|  
|**Nicht zwischengespeichert. Für Datensammlung und -upload wird derselbe Zeitplan verwendet.**|Wenn diese Option aktiviert ist, geben Sie einen der folgenden Werte an:<br /><br /> **Zeitplan** Daten werden nach einem Zeitplan aufgelistet und hochgeladen. Klicken Sie auf **Auswählen** , um einen vordefinierten Zeitplan aus der Liste auszuwählen, oder klicken Sie auf **Neu** , um einen neuen Zeitplan zu erstellen.<br /><br /> **Bedarfsgesteuert**. Daten werden nach Bedarf aufgelistet und hochgeladen.|  
|**Zwischengespeichert. Sammeln und Zwischenspeichern von Daten gemäß bestimmten Sammlungshäufigkeiten. Zwischengespeicherte Daten werden gemäß einem separaten Zeitplan hochgeladen.**|Daten werden gemäß bestimmten Sammlungshäufigkeiten aufgelistet und zwischengespeichert. Die aufgelisteten Daten werden gemäß einem separaten Zeitplan hochgeladen.|  
  
 **Sammelhäufigkeit (Sek)**  
 Zeigt die Sammelelemente im Sammlungssatz an. Die folgenden Informationen werden für jedes Sammelelement bereitgestellt:  
  
-   **Name**  
  
-   **Sammlertyp**  
  
-   **Sammlungshäufigkeit** (Sek). Dieses Feld ist bearbeitbar, wenn **Datensammlung und -upload** als zwischengespeichert konfiguriert ist. Doppelklicken Sie auf diese Zelle, um die Sammlungshäufigkeit festzulegen.  
  
 **Eingabeparameter**  
 Zeigt die für den Sammlungssatz verwendeten Eingabeparameter an.  
  
 **Ausführen als**  
 Gibt das Konto an, das verwendet wird, um den Sammlungssatz auszuführen. Dies entspricht standardmäßig dem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienstkonto. Wenn Proxykonten definiert sind, enthält diese Liste die Namen der verfügbaren Proxykonten.  
  
 **Festlegen, wie lang gesammelte Daten im Verwaltungs-Data Warehouse beibehalten werden**  
 Gibt an, wie lange aufgelistete Daten beibehalten werden. Wählen Sie eine der folgenden Optionen aus.  
  
|||  
|-|-|  
|**Daten beibehalten für**|Diese Option ist standardmäßig aktiviert, und die Standardbeibehaltungsdauer ist 14 Tage.|  
|**Daten unbegrenzt beibehalten**|Daten können für unbegrenzte Zeit beibehalten werden.|  
  
 **Uploads (Seite)**  
  
 Auf dieser Seite können Sie den Uploadzeitplan für Daten konfigurieren, die von diesem Sammlungssatz aufgelistet werden.  
  
> [!NOTE]  
>  Diese Registerkarte ist nur aktiviert, wenn die Option **Zwischengespeichert** für **Datensammlung und -upload**konfiguriert wurde.  
  
 **Server**  
 Zeigt den Namen des Servers an, der als Host für das Verwaltungs-Data Warehouse fungiert. Weitere Informationen finden Sie unter [Konfigurieren des Verwaltungs-Data Warehouses &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Verwaltungs-Data Warehouse**  
 Zeigt den Namen des Verwaltungs-Data Warehouses an. Weitere Informationen finden Sie unter [Konfigurieren des Verwaltungs-Data Warehouses &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md).  
  
 **Letzter Upload**  
 Zeigt Datums- und Uhrzeitinformationen zum letzten für den Sammlungssatz ausgeführten Upload an.  
  
 **Uploadzeitplan**  
 Gibt den Uploadzeitplan für den Sammlungssatz an. Wenn diese Option aktiviert ist, klicken Sie auf **Auswählen** , um einen vordefinierten Zeitplan aus der Liste auszuwählen, oder klicken Sie auf **Neu** , um einen neuen Zeitplan zu erstellen.  
  
 **Beschreibung (Seite)**  
  
 Auf dieser Seite können Sie eine Beschreibung des Sammlungssatzes anzeigen, auf den diese Eigenschaftenseite verweist.  
  
## <a name="see-also"></a>Siehe auch  
 [Verwalten von Datensammlungen](../../relational-databases/data-collection/manage-data-collection.md)   
 [Datensammlung](../../relational-databases/data-collection/data-collection.md)  
  
  
