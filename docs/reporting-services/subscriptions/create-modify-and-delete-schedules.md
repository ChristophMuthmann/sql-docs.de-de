---
title: "Erstellen, ändern und Löschen von Zeitplänen | Microsoft Docs"
ms.custom: 
ms.date: 07/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services]
- modifying schedules
- removing schedules
- shared schedules [Reporting Services], creating
- shared schedules [Reporting Services], modifying
- schedules [Reporting Services], deleting
- deleting schedules
- schedules [Reporting Services], creating
- schedules [Reporting Services], modifying
- shared schedules [Reporting Services], deleting
ms.assetid: 05da5f3d-9222-43a9-893b-aa10f0f690f8
caps.latest.revision: 50
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 66a306d07b8556fe43659d4b078e2d31f3d51900
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="create-modify-and-delete-schedules"></a>Erstellen, Ändern oder Löschen von Zeitplänen
  In diesem Hilfethema erhalten Sie Informationen zum Erstellen, Ändern und Löschen von freigegebenen [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] -Zeitplänen.  Freigegebene Zeitpläne für den einheitlichen Modus werden auf der Seite „Zeitpläne“ im Webportal oder im Ordner „Freigegebene Zeitpläne“ in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]verwaltet. Verwenden Sie für den SharePoint-Modus die Verwaltungsseiten für die [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Dienstanwendung.  
  
 Verwenden Sie eine der folgenden Methoden, um festzustellen, ob ein freigegebener Zeitplan aktiv verwendet wird:  
  
-   **Webportal:** Prüfen Sie die Werte in den Feldern „Zuletzt ausgeführt am“, „Nächste Ausführung“ und „Status“ auf der Seite „Freigegebene Zeitpläne“. Wenn ein Zeitplan nicht mehr ausgeführt wird, weil er abgelaufen ist, wird das Ablaufdatum im Feld Status angezeigt. Weitere Informationen finden Sie unter [Web portal (SSRS Native Mode)](../../reporting-services/web-portal-ssrs-native-mode.md).
  
-   **[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)]:** Anzeigen der Seite „Berichte“ eines bestimmten freigegebenen Zeitplans. Auf dieser Seite werden alle Berichte und freigegebenen Datasets aufgeführt, die den freigegebenen Zeitplan verwenden. Weitere Informationen finden Sie unter [Reporting Services in SQL Server Management Studio ](../../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md).
  
-  **Protokolle:** Anzeigen der Protokolldateien oder Ablaufverfolgungsprotokolle der Berichtsausführung, um zu ermitteln, ob Berichte zu den im Zeitplan angegebenen Zeiten ausgeführt wurden. Weitere Informationen finden Sie unter [Reporting Services-Protokolldateien und Quellen](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="when-you-delete-a-shared-schedule"></a>Löschen eines freigegebenen Zeitplans  
Freigegebene Zeitpläne müssen mit der Seite „Zeitplan“ im Webportal oder dem Ordner „Freigegebene Zeitpläne“ in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]manuell gelöscht werden. Wenn Sie einen freigegebenen Zeitplan löschen, der verwendet wird, werden alle Verweise darauf durch berichtsspezifische Zeitpläne ersetzt.  
 
Wenn Sie einen freigegebenen Zeitplan löschen, der von mehreren Berichten und Abonnements verwendet wird, erstellt der Berichtsserver für Berichte und Abonnements, die vorher den freigegebenen Zeitplan verwendet haben, eigene Zeitpläne. Jeder dieser neuen Zeitpläne enthält das Datum, die Zeit und die Wiederholungsoption, die in dem freigegebenen Zeitplan angegeben wurden. Beachten Sie, dass [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] keine zentrale Verwaltung für einzelne Zeitpläne bereitstellt. Wenn Sie einen freigegebenen Zeitplan löschen, müssen Sie jetzt die Zeitplaninformationen für jedes einzelne Element verwalten.  
  
**Hinweis:**  Wenn Sie nicht sicher sind, ob ein freigegebener Zeitplan verwendet wird, sollten Sie diesen ggf. in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] statt im Webportal löschen. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] bietet die gleichen Verwaltungsfunktionen für freigegebene Zeitpläne wie der Berichts-Manager, verfügt aber zusätzlich über eine Berichtsseite mit dem Namen jedes Bericht, der den Zeitplan verwendet.  
   
 Das Löschen eines Zeitplans und das Ablaufen eines Zeitplans sind zwei unterschiedliche Dinge. Mithilfe eines Ablaufzeitpunktes wird ein Zeitplan beendet, aber nicht gelöscht. Da Zeitpläne für die Automatisierung vieler Funktionen verwendet werden, werden sie niemals automatisch gelöscht. Abgelaufene Zeitpläne stellen Berichtsserveradministratoren Hinweise bereit, weshalb ein automatisierter Prozess plötzlich beendet wurde. Ohne den abgelaufenen Zeitplan könnte der Berichtsserveradministrator eine falsche Diagnose des Problems stellen oder unnötig Zeit mit der Problembehandlung eines voll funktionsfähigen Prozesses verschwenden.  
 
 ## <a name="when-you-delete-a-report-specific--schedule"></a>Löschen eines berichtsspezifischen Zeitplans  
Berichts- und abonnementspezifische Zeitpläne werden beim Löschen eines Berichts oder Abonnements oder bei der Auswahl einer anderen Vorgehensweise zum Ausführen des Berichts bzw. des Abonnements gelöscht. So wird beispielsweise mit **Diesen Bericht immer mit den neuesten Daten ausführen** ein berichtsspezifischer Zeitplan gelöscht, den Sie für die Ausführung eines Berichts als Berichtsausführungs-Momentaufnahme erstellt haben.  

Ein abgelaufener berichtsspezifischer Zeitplan bleibt weiterhin mit dem Bericht verbunden. Durch Überprüfen des Enddatums können Sie ermitteln, ob ein Zeitplan abgelaufen ist. Ein abgelaufener freigegebener Zeitplan verbleibt in der Liste Freigegebene Zeitpläne. Das Feld Status zeigt an, ob der Zeitplan abgelaufen ist. Sie können den Zeitplan wiederherstellen, indem Sie das Enddatum des Zeitplans verlängern, oder Sie löschen den Zeitplanverweis, wenn er nicht mehr benötigt wird.  
  
## <a name="bkmk_native"></a> Erstellen, Löschen oder Ändern eines freigegebenen Zeitplans (Webportal)  
 Beim Erstellen und Ändern eines Zeitplans werden Optionen festgelegt, die bestimmen, wann der Zeitplan ausgeführt wird.  
  
 Einen Zeitplan können Sie jederzeit erstellen oder ändern. Wenn jedoch ein Zeitplan vor Abschluss Ihrer Änderungen ausgeführt wird, wird die vorherige Version des Zeitplans verwendet. Der geänderte Zeitplan wird erst nach dem Speichern wirksam.  
  
 Wenn Sie einen freigegebenen Zeitplan ändern, können Sie ihn anhalten, bevor Sie Änderungen daran vornehmen. Die Änderungen werden wirksam, wenn Sie den Zeitplan fortsetzen.  

1.  Klicken Sie im Webportal auf **Einstellungen** ![ssrs_portal_settings_gear](../../reporting-services/subscriptions/media/ssrs-portal-settings-gear.png) in der Symbolleiste. **Hinweis:** Falls die Option **Siteeinstellungen** nicht verfügbar ist, haben Sie keine Zugriffsberechtigung für die Siteeinstellungen.
2.  Klicken Sie auf **Siteeinstellungen**.  
3.  Klicken Sie auf **Zeitpläne**.  
4.  Klicken Sie auf **Neuer Zeitplan**. Klicken Sie zum Ändern eines vorhandenen Zeitplans auf den Namen des Zeitplans.  
5.  Geben Sie einen beschreibenden Namen für den Zeitplan ein.  
6.  Wählen Sie **Stunde**, **Tag**, **Woche**oder **Monat**aus. Klicken Sie auf **Einmal** , um einen einmaligen Zeitplan zu erstellen. Wenn Sie die Basis Ihres Zeitplans angeben, werden zusätzliche Optionen angezeigt.  
7.  Wählen Sie optional ein Datum aus, an dem der Zeitplan starten soll. Der Standardwert ist der aktuelle Tag. Sie können den Startzeitpunkt des Zeitplans verschieben, indem Sie ein späteres Datum auswählen.  
8.  Wählen Sie optional ein Datum aus, an dem der Zeitplan enden soll. An diesem Datum wird die Ausführung des Zeitplans angehalten, der Zeitplan wird jedoch nicht gelöscht.  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="to-delete-a-shared-schedule-web-portal"></a>So löschen Sie einen freigegebenen Zeitplan (Webportal)  
  
1.  Klicken Sie im Webportal auf der globalen Symbolleiste auf **Siteeinstellungen**.     
2.  Klicken Sie auf der Seite im Bereich **Sonstige** auf **Freigegebene Zeitpläne verwalten**.  
3.  Aktivieren Sie das Kontrollkästchen neben dem zu löschenden Zeitplan, und klicken Sie dann auf **Löschen**.  
  
### <a name="create-delete-or-modify-a-shared-schedule-management-studio"></a>Erstellen, Löschen oder Ändern eines freigegebenen Zeitplans (Management Studio)  
 Ein freigegebener Zeitplan enthält Informationen zum Zeitplan und zu Wiederholungen, die von einer beliebigen Anzahl veröffentlichter Berichte und Abonnements verwendet werden können, die auf einem [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver ausgeführt werden. Werden zahlreiche Berichte und Abonnements gleichzeitig ausgeführt, können Sie für diese Aufträge einen freigegebenen Zeitplan erstellen. Soll zu einem späteren Zeitpunkt das Wiederholungsmuster oder das Enddatum geändert werden, können Sie diese Änderung für alle Berichte und Abonnements an einer Stelle vornehmen.  
  
 Freigegebene Zeitpläne sind leichter zu verwalten und ermöglichen Ihnen eine größere Flexibilität in der Verwaltung geplanter Vorgänge. So besteht beispielsweise die Möglichkeit, freigegebene Zeitpläne zu beenden und fortzusetzen. Wenn Sie der Ansicht sind, dass zu viele geplante Vorgänge gleichzeitig ausgeführt werden, können Sie mehrere freigegebene Zeitpläne erstellen, die zu verschiedenen Zeitpunkten ausgeführt werden, und anschließend die Zeitplaninformationen entsprechend der Verarbeitungslast auf dem Berichtsserver anpassen.  
  
### <a name="to-create-or-modify-a-shared-schedule-management-studio"></a>So erstellen oder ändern Sie einen freigegebenen Zeitplan (Management Studio)  
  
1.  Starten Sie [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] , und stellen Sie eine Verbindung zu einer Berichtsserverinstanz her.  
2.  Erweitern Sie im Objekt-Explorer einen Berichtsserverknoten.  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Freigegebene Zeitpläne** , und klicken Sie anschließend auf **Neuer Zeitplan**. Die Seite Allgemein im Dialogfeld **Neuer freigegebener Zeitplan** wird angezeigt.  
  
     Erweitern Sie zum Ändern eines vorhandenen freigegebenen Zeitplans den Ordner „Freigegebene Zeitpläne“, klicken Sie mit der rechten Maustaste auf den gewünschten Zeitplan, und klicken Sie anschließend auf **Eigenschaften**.  
  
4.  Geben Sie einen beschreibenden Namen für den Zeitplan ein.  
5.  Wählen Sie optional ein Datum aus, an dem der Zeitplan starten soll. Der Standardwert ist der aktuelle Tag.  
6.  Wählen Sie optional ein Datum aus, an dem der Zeitplan enden soll. An diesem Datum wird die Ausführung des Zeitplans angehalten, der Zeitplan wird jedoch nicht gelöscht.  
7.  Sie können Wiederholungen des Zeitplans konfigurieren, indem Sie **Stunde**, **Tag**, **Woche**oder **Monat**auswählen. Es werden zusätzliche Optionen angezeigt. Verwenden Sie diese Zusatzoptionen, um die Häufigkeit der Zeitplanausführung auf der Grundlage der von Ihnen bevorzugten Angabe für Stunde, Tag, Woche oder Monat zu konfigurieren.  
  
     Oder geben Sie einen einmaligen (nicht wiederkehrenden) Zeitplan an, indem Sie **Einmal**auswählen und anschließend eine **Startzeit**angeben.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##### <a name="to-delete-a-shared-schedule-management-studio"></a>So löschen Sie einen freigegebenen Zeitplan (Management Studio)  
  
1.  Erweitern Sie im Objekt-Explorer einen Berichtsserverknoten.  
2.  Erweitern Sie den Ordner „Freigegebene Zeitpläne“, klicken Sie mit der rechten Maustaste auf den Zeitplan, und klicken Sie auf **Eigenschaften**, um sicherzustellen, dass der freigegebene Zeitplan derzeit nicht von Berichten verwendet wird.
3. Klicken Sie auf die Registerkarte **Berichte** , um die Liste der Berichte anzuzeigen, die den Zeitplan derzeit verwenden.
Klicken Sie auf **Abbrechen**.
4.  Erweitern Sie den Ordner „Freigegebene Zeitpläne“, klicken Sie mit der rechten Maustaste auf den zu löschenden Zeitplan, und klicken Sie anschließend auf **Löschen**. Das Dialogfeld **Katalogelemente löschen** wird angezeigt.  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
 Wenn Sie einen freigegebenen Zeitplan löschen, der von mehreren Berichten und Abonnements verwendet wird, erstellt der Berichtsserver für Berichte und Abonnements, die vorher den freigegebenen Zeitplan verwendet haben, eigene Zeitpläne. Jeder dieser neuen Zeitpläne enthält das Datum, die Zeit und die Wiederholungsoption, die in dem freigegebenen Zeitplan angegeben wurden.
 
##  <a name="bkmk_sharepoint"></a> Erstellen und Verwalten von freigegebenen Zeitplänen (SharePoint-Modus)  
 Sie müssen ein Websiteadministrator sein, um freigegebene Zeitpläne auf einer SharePoint-Website erstellen, ändern oder löschen zu können.  
  
 Sie können einen bestimmten Zeitplan an seinem beschreibenden Namen identifizieren. Wenn kein Name angegeben ist, wird ein Standardname erstellt, der auf Fakten zum Zeitplan (z. B. sein Serienmuster oder Datum und Uhrzeit der Ausführung) basiert.  
  
> [!NOTE]  
>  Das Erstellen freigegebener Zeitpläne erfordert den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent-Dienst.  
  
### <a name="create-shared-schedules-sharepoint-mode"></a>Erstellen von freigegebenen Zeitplänen (SharePoint-Modus)  
1.  Klicken Sie auf **Websiteaktionen**.  
2.  Klicken Sie auf **Siteeinstellungen**.  
3.  Klicken Sie im Abschnitt **Reporting Services**auf Freigegebene Zeitpläne verwalten.  
4.  Klicken Sie auf **Zeitplan hinzufügen** , um die Seite Zeitplaneigenschaften zu öffnen.  
5.  Geben Sie einen beschreibenden Namen für den Zeitplan ein. Auf den Anwendungsseiten, die für das Arbeiten mit [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichten verwendet werden, wird dieser Name in Dropdownlisten auf Seiten für Zeitplandefinitionen auf der gesamten Website angezeigt. Vermeiden Sie lange Namen, die schwer lesbar sind. Folgen Sie einer Benennungskonvention, bei der die meisten Beschreibungsinformationen an den Anfang des Namens gestellt werden.  
6.  Wählen Sie eine Häufigkeit aus. In Abhängigkeit von der von Ihnen ausgewählten Häufigkeit werden auf der Seite möglicherweise unterschiedliche Zeitplanoptionen angezeigt, mit denen die entsprechende Häufigkeit unterstützt wird. Wenn Sie beispielsweise **Monat**auswählen, werden alle Monatsnamen auf der Seite angezeigt.  
7.  Definieren Sie den Zeitplan. Nicht alle Zeitplankombinationen können in einem einzelnen Zeitplan unterstützt werden.  
8.  Legen Sie ein Start- und Enddatum fest.  
9. Klicken Sie auf **OK**.  
  
### <a name="delete-shared-schedules-sharepoint-mode"></a>Löschen von freigegebenen Zeitplänen (SharePoint-Modus)  
 Alle Zeitpläne, ob freigegeben oder berichtsspezifisch, müssen manuell gelöscht werden. Wenn Sie einen freigegebenen Zeitplan löschen, der gerade verwendet wird, werden allen Verweise auf ihn durch benutzerdefinierte Zeitpläne ohne Angabe ersetzt (d. h. durch einen benutzerdefinierten Bericht, für den keine Datums- oder Uhrzeitinformationen verfügbar sind).  
  
1.  Klicken Sie auf **Websiteaktionen**.  
2.  Klicken Sie auf **Siteeinstellungen**.  
3.  Klicken Sie im Abschnitt **Reporting Services**auf Freigegebene Zeitpläne verwalten.  
4.  Wählen Sie den Zeitplan aus, und klicken Sie auf **Löschen**.  
 
  
## <a name="see-also"></a>Siehe auch  
 [Schedules](../../reporting-services/subscriptions/schedules.md)   
 [Anhalten und Fortsetzen von freigegebenen Zeitplänen](../../reporting-services/subscriptions/pause-and-resume-shared-schedules.md)   
 [Zwischenspeichern eines Berichts &#40; Berichts-Manager &#41;](../../reporting-services/report-server/cache-a-report-report-manager.md)   
 [Hinzufügen einer Momentaufnahme zum Melden von Sicherungsverlauf &#40; Berichts-Manager &#41;](../../reporting-services/report-server/add-a-snapshot-to-report-history-report-manager.md)  
  
  

