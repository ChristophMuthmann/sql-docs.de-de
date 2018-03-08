---
title: "Wartungsplan (Registerkarte „Entwurf“) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.maint.maintplanproperties.optimizations.f1
- sql13.swb.maint.planeditor.f1
- sql13.swb.maint.subplaneditor.f1
ms.assetid: 6d20d4d4-5b3f-454a-8a05-f0aac803c5ad
caps.latest.revision: "27"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e425cd4e4901b396ae08cc9586381120ab225745
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2018
---
# <a name="maintenance-plan-design-tab"></a>Wartungsplan (Registerkarte Entwurf)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Verwenden Sie **Wartungsplan (Registerkarte „Entwurf“)**, um die Eigenschaften eines Wartungsplans und seiner Unterpläne anzugeben. Ziehen Sie Tasks aus der Toolbox in den Wartungsplan-Designer. Klicken Sie mit der rechten Maustaste auf Gruppen von Tasks, um verzweigte Ausführungspfade zu erstellen. Wartungspläne werden als [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakete gespeichert, die von Aufträgen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agents ausgeführt werden.  
  
## <a name="options"></a>Tastatur  
 **Unterplan hinzufügen**  
 Mit dieser Option fügen Sie einen Unterplan hinzu, den Sie konfigurieren können.  
  
 **Unterplaneigenschaften**  
 Hiermit zeigen Sie das Dialogfeld **Unterplaneigenschaften** an. Wählen Sie einen Unterplan im Raster aus, und klicken Sie auf dieses Symbol, um einen Namen, eine Beschreibung und einen Zeitplan für den Unterplan einzugeben. Sie können auch auf den Unterplan im Raster doppelklicken, um das Dialogfeld **Unterplaneigenschaften** anzuzeigen. Unterplannamen sind auf 128 Zeichen beschränkt, und Beschreibungen für Unterpläne dürfen höchstens 512 Zeichen umfassen.  
  
 **Ausgewählten Unterplan löschen**  
 Hiermit löschen Sie den ausgewählten Unterplan.  
  
 **Zeitplan des Unterplans**  
 Hiermit zeigen Sie das Dialogfeld **Eigenschaften des Auftragszeitplans** an. Wählen Sie einen Unterplan im Raster aus, und klicken Sie auf dieses Symbol, um einen Zeitplan für den Unterplan zu konfigurieren.  
  
 **Zeitplan entfernen**  
 Mit dieser Option entfernen Sie einen Zeitplan aus dem ausgewählten Unterplan.  
  
 **Verbindungen verwalten**  
 Hiermit zeigen Sie das Dialogfeld **Verbindungen verwalten** an. Es wird verwendet, um dem Wartungsplan zusätzliche [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Instanzverbindungen hinzuzufügen. Jeder Wartungstask im Unterplan-Editor kann beliebige dieser Verbindungen nutzen. Bei der Ausführung stellt der Wartungsplan eine Verbindung vom Wartungsplanserver zu den angegebenen Servern mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] her, wobei die Anmeldeinformationen der Verbindungen verwendet werden.  
  
 **Berichterstellung und Protokollierung**  
 Hiermit zeigen Sie das Dialogfeld **Berichterstellung und Protokollierung** an, das zur Verwaltung von Berichten bezüglich der Wartungsplanaktivitäten und zur Konfigurierung der Protokollierung auf dem lokalen Server oder auf einem Remoteserver verwendet wird.  
  
 **Server**  
 Mit dieser Option zeigen Sie das Dialogfeld **Server** an, das zum Auswählen der Server verwendet wird, auf denen die Unterplantasks ausgeführt werden. Diese Option ist nur auf Masterservern in Umgebungen mit mehreren Servern aktiviert. Weitere Informationen finden Sie unter [Erstellen einer Multiserverumgebung](http://msdn.microsoft.com/library/edc2b60d-15da-40a1-8ba3-f1d473366ee6).  
  
 **Name**  
 Hier zeigen Sie den Namen für den Wartungsplan an. Bei neuen Wartungsplänen wird der Name in einem Dialogfeld angegeben, bevor der Designer für den Wartungsplan geöffnet wird. Wenn Sie einen Wartungsplan umbenennen möchten, klicken Sie im Objekt-Explorer mit der rechten Maustaste auf den Plan, und klicken Sie anschließend auf **Umbenennen**.  
  
 **Beschreibung**  
 Hier können Sie eine Beschreibung für den Wartungsplan anzeigen oder festlegen. Die maximale Länge für eine Beschreibung beträgt 512 Zeichen.  
  
 **Designeroberfläche**  
 Hiermit können Sie Wartungspläne entwerfen und verwalten. Verwenden Sie die Designeroberfläche, um einem Plan Wartungspläne hinzuzufügen, Tasks aus einem Plan zu entfernen, Rangfolgenlinks zwischen den Tasks anzugeben oder Taskverzweigungen und -parallelausführungen anzuzeigen.  
  
 Ein Rangfolgenlink zwischen zwei Tasks legt eine Beziehung zwischen den Tasks fest. Der zweite Task (der *abhängige Task*) wird nur ausgeführt, wenn das Ausführungsergebnis des ersten Tasks (des *Vorgängertasks*) bestimmte Kriterien erfüllt. Normalerweise ist das angegebene Ausführungsergebnis **Erfolg**, **Fehler**oder **Beendigung**. Die Oberfläche des Wartungsplan-Designers basiert auf der Oberfläche des [!INCLUDE[ssIS](../../includes/ssis-md.md)] -Designers. Weitere Informationen finden Sie unter [Rangfolgeneinschränkungen](../../integration-services/control-flow/precedence-constraints.md).  
  
 Ein Task zur Defragmentierung des Indexes könnte beispielsweise so festgelegt werden, dass er nur ausgeführt wird, wenn der vorher ausgeführte Task Datenbankintegrität überprüfen erfolgreich abgeschlossen wurde. Mit der Funktion für Rangfolgenlinks werden Fehlerbehandlungen und Vorgehensweisen bei Fehlschlägen in den Plänen ermöglicht. Bei einem Fehler des Tasks Datenbankintegritätsprüfung könnte der Task Operator benachrichtigen beispielsweise einen Benutzer oder Operator über den Fehler benachrichtigen.  
  
 Das Festlegen eines auszuführenden Tasks für den Fall eines Fehlers beim vorangegangenen Task ist ein Beispiel für eine *Taskverzweigung*.  
  
 Wenn die Ausführung mehrerer Tasks gleichzeitig beginnt, z. B. nach dem erfolgreichen Abschluss eines Vorgängertasks, dann ist diese Festlegung ein Beispiel für *Taskparallelität*. Alle Tasks ohne Einschränkungen werden parallel gestartet und ausgeführt. Verwenden Sie Einschränkungen, um Tasks zu verzögern, damit frühere Tasks vorher abgeschlossen werden.  
  
 Nachdem ein Wartungstask auf der Entwurfsoberfläche platziert ist, können seine Eigenschaften je nach Bedarf bearbeitet werden. So wird beispielsweise die für einen Task Datenbank sichern relevante Datenbank erst angegeben, nachdem der Task dem Plan hinzugefügt wurde. Die Tasks auf der Entwurfsoberfläche, die nicht ordnungsgemäß konfiguriert sind, enthalten ein rotes Symbol mit einem weißen x.  
  
 Wenn Sie einem Plan einen Wartungstask hinzufügen möchten, ziehen Sie das Symbol des Tasks aus der Toolbox **Wartungsplantasks** in die Planentwurfsoberfläche, oder doppelklicken Sie in der Toolbox auf den Task, wodurch dieser Task der derzeit aktiven Designeroberfläche hinzugefügt wird. Wenn die im Menü **Wartungsplantasks** nicht sichtbar ist, wählen Sie in **im Menü** Ansicht [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Toolbox** aus. Erweitern Sie den Knoten **Wartungsplantasks** im Bereich **Toolbox** .  
  
 Wenn Sie einen Task aus einem Plan entfernen möchten, wählen Sie den Task in der Designeroberfläche aus, und drücken Sie die **ENTF** -TASTE, oder klicken Sie mit der rechten Maustaste auf den Task, und klicken Sie auf **Löschen**.  
  
 Wenn Sie Rangfolgenlinks zwischen zwei Tasks angeben möchten, ziehen Sie die Tasks zunächst auf die Entwurfsoberfläche, klicken Sie anschließend auf den zuerst auftretenden Task (den Vorgängertask), und ziehen Sie anschließend den Pfeil auf den abhängigen Task. Wenn ein Rangfolgenlink eingerichtet wurde, zeigt der Designer einen Pfeil an, der die beiden Tasks miteinander verbindet, wobei der Vorgängertask auf den abhängigen Task zeigt. Wenn ein Link erstmalig eingerichtet wird, sind die Einschränkungen für den Link so festgelegt, dass der abhängige Task nur ausgeführt wird, wenn das Ausführungsergebnis des Vorgängertasks **Erfolg**ist.  
  
 Um die Eigenschaften eines Rangfolgenlinks zu ändern, doppelklicken Sie auf den Link, um den **Rangfolgeneinschränkungs-Editor**zu starten. Hier werden viele Optionen für das Festlegen logischer Bedingungen bereitgestellt, die bestimmen, ob der abhängige Task ausgeführt wird. Das **Ausführungsergebnis** kann z. B. auf **Fehler**festgelegt werden, wodurch der abhängige Task nur ausgeführt wird, wenn der Vorgängertask fehlschlägt. Die Änderung der Ausführungsergebnis-Eigenschaft eines Links in **Erfolg**, **Fehler**oder **Beendigung**kann auch vorgenommen werden, indem Sie mit der rechten Maustaste auf den Link klicken und dann die entsprechende Option im Kontextmenü auswählen.  
  
 Um eine Taskverzweigung festzulegen, erstellen Sie zunächst Rangfolgenlinks zwischen zwei Tasks. Platzieren Sie dann einen weiteren abhängigen Task auf der Entwurfsoberfläche, der bei einem anderen Ergebnis als der erste abhängige Task ausgeführt werden soll. Klicken Sie auf den Vorgängertask, und ziehen Sie den zweiten Pfeil vom Vorgängertask auf den abhängigen Task. Wenn Sie das Ausführungsergebnis (**Erfolg**, **Fehler**, **Beendigung**), das zur Ausführung eines abhängigen Tasks führt, ändern möchten, doppelklicken Sie auf den Linkpfeil, und ändern Sie das Feld **Ausführungsergebnis** . Alternativ dazu können Sie auch mit der rechten Maustaste auf den Link klicken und den gewünschten Ausführungsergebniswert aus dem Kontextmenü auswählen.  
  
 Um Taskparallelitäten festzulegen, verknüpfen Sie mehrere abhängige Tasks mit einem einzelnen Vorgängertask. Ändern Sie die Eigenschaften der Rangfolgenlinks so, dass diejenigen, die auf die parallel auszuführenden abhängigen Tasks zeigen, denselben Wert in den Ausführungsergebnisfeldern haben.  
  
## <a name="additional-features-available-from-the-shortcut-menu"></a>Zusätzlich verfügbare Funktionen im Kontextmenü  
 Um zusätzliche Optionen anzuzeigen, wählen Sie einen oder mehrere Tasks auf der Entwurfsoberfläche aus, und klicken Sie mit der rechten Maustaste auf die Auswahl, um das Kontextmenü zu öffnen. Zusätzlich zu den üblichen Optionen **Ausschneiden**, **Kopieren**, **Einfügen**, **Löschen**und **Alles auswählen**sind folgende besondere Optionen für einige Tasks verfügbar.  
  
 **Anmerkung hinzufügen**  
 Fügt der Entwurfsoberfläche eine beschreibende Anmerkung hinzu.  
  
 **Bearbeiten**  
 Öffnet das Eigenschaftendialogfeld für den Task.  
  
 **Deaktivieren**  
 Sorgt dafür, dass der Task vorübergehend nicht verfügbar ist.  
  
 **Aktivieren**  
 Stellt einen zuvor deaktivierten Task wieder her.  
  
 **Gruppe**  
 Erstellt eine Gruppe, die einen oder mehrere Tasks enthält.  
  
 **Gruppierung aufheben**  
 Entfernt Tasks aus einer Gruppe.  
  
 **Automatisch anpassen**  
 Legt die Größe aller Tasks auf das jeweilige Optimum fest.  
  
 **Reduzieren**  
 Blendet Tasks innerhalb einer Gruppe aus.  
  
 **Erweitern**  
 Zeigt die Tasks in einer Gruppe an, die zuvor mithilfe der Option **Reduzieren**ausgeblendet wurden.  
  
 **Zoom**  
 Ändert die Größe der Tasks auf der Entwurfsoberfläche.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Wartungspläne](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Erstellen eines Wartungsplans](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
  
