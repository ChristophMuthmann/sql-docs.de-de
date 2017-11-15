---
title: "Importieren von Bereinigungsprojektwerten in eine Domäne | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: data-quality-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.dqs.kb.importprojectvalues.f1
ms.assetid: f23e38e2-39e0-42d7-abd5-34d8fcca5d2a
caps.latest.revision: "21"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c08c593ddefd7b45de422630f696ba020509f052
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="import-cleansing-project-values-into-a-domain"></a>Importieren von Bereinigungsprojektwerten in eine Domäne
  In [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) können Sie während des Bereinigungsprozesses in einem Datenqualitätsbereinigungsprojekt oder einem Integration Services-Paket mit der DQS-Bereinigungskomponente erfasstes Datenqualitätswissen in eine Domäne importieren. Dadurch wird sichergestellt, dass vertrauenswürdiges Wissen nicht verloren geht und dass die Wissensdatenbank ständig verbessert wird.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
  
-   Zum Importieren von Bereinigungsprojektwerten in eine Domäne muss die Domäne im Bereinigungsprojekt in Data Quality Client oder dem Integration Services-Paket, das eine DQS-Bereinigungs-Komponente enthält, verwendet worden sein.  
  
-   Das Bereinigungsprojekt in Data Quality Client oder dem Integration Services-Paket mit der DQS-Bereinigungskomponente muss erfolgreich abgeschlossen worden sein.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_kb_editor“ oder „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um während des Bereinigungsprozesses gesammeltes Data Quality-Wissen in eine Domäne zu importieren.  
  
##  <a name="Import"></a> Importieren von Bereinigungsprojektwerten  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Öffnen Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm in der Domänenverwaltungsaktivität eine Wissensdatenbank.  
  
3.  Wenn Sie einer vorhandenen Domäne Werte hinzufügen, wählen Sie die Domäne in der Domänenliste aus.  
  
4.  Klicken Sie auf die Registerkarte **Domänenwerte** , klicken Sie auf das Symbol **Werte importieren** in der Symbolleiste, und klicken Sie dann auf **Projektwerte importieren**. Das Dialogfeld **Projektwerte importieren** wird mit einer Liste von Data Quality-Projekten und Integration Services-Paketen angezeigt, die mit der Domäne bereinigt wurden.  
  
    > [!NOTE]  
    >  Wenn kein Projekt mit der Domäne oder einer verknüpften Domäne erstellt wurde oder das Projekt nicht abgeschlossen wurde, ist die Option **Projektwerte importieren** nicht verfügbar.  
  
5.  Im Dialogfeld **Projektwerte importieren** :  
  
    -   Wählen Sie in der Dropdownliste **Importiert** die Option **Alle** aus, um alle Projekte anzuzeigen, oder **Nein** , um nur die Projekte anzuzeigen, deren Werte noch nicht importiert wurden.  
  
    -   Wählen Sie das Projekt aus, aus dem Sie Werte importieren möchten.  
  
    -   Wählen Sie **Werte aus der Registerkarte 'Neu' hinzufügen** aus, um Werte, zusätzlich zu Werten auf den Registerkarten **Richtig** und **Korrigiert** , in die neue Registerkarte zu importieren.  
  
    -   Klicken Sie auf **OK**.  
  
6.  Die Registerkarte **Domänenwerte** wird wieder angezeigt, und es wird eine Meldung zum erfolgreichen Importieren der Werte angezeigt. Werte, die importiert wurden und deshalb neu in der Domäne sind, werden in der Tabelle **Werte** angezeigt.  
  
7.  Deaktivieren Sie **Nur neue anzeigen** , um alle Werte in der Domäne anzuzeigen.  
  
8.  Wählen Sie **Richtig**, **Fehler**oder **Ungültig** aus, um nur die Werte mit dem ausgewählten Typ anzuzeigen.  
  
9. Um nach einer bestimmten Zeichenfolge zu suchen, geben Sie die Zeichenfolge in das Textfeld **Suchen** ein. Klicken Sie auf den Pfeil nach oben oder nach unten, um durch die Werte zu blättern, die die Suchkriterien erfüllen. Sie werden in Gelb hervorgehoben.  
  
10. Klicken Sie auf **Fertig stellen**.  
  
    > [!NOTE]  
    >  Weitere Informationen zum Arbeiten mit Werten auf der Registerkarte **Domänenwerte** finden Sie unter [Change Domain Values](../data-quality-services/change-domain-values.md).  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Importieren von Projektwerten in eine Domäne  
 Nachdem Sie während des Bereinigungsprozesses gesammeltes Data Quality-Wissen in eine Domäne importiert haben, können Sie andere Domänenverwaltungsaufgaben für die Domäne und die Werte ausführen. Weitere Informationen finden Sie unter [Verwalten einer Domäne](../data-quality-services/managing-a-domain.md).  
  
##  <a name="Values"></a> Importierte Werte  
 Die folgenden Werte werden aus einem Projekt in eine Domäne importiert:  
  
-   Nur Zeichenfolgenwerte werden in die Domäne importiert.  
  
-   Nur Werte aus den Registerkarten **Richtig**, **Korrigiert**und **Neu** auf der Seite **Ergebnisse verwalten und anzeigen** der **Bereinigungsaktivität** werden importiert. Werte auf der Registerkarte **Neu** werden nur importiert, wenn das Kontrollkästchen **Werte aus der Registerkarte 'Neu' hinzufügen** im Dialogfeld **Projektwerte importieren** aktiviert wurde.  
  
-   Werte werden als richtig oder als Fehler mit der Korrektur importiert. Nur ein Fehlerwert mit einem Korrekturwert wird importiert.  
  
-   Der Korrekturwert ist entweder ein neuer Wert, der in der Wissensdatenbank nicht vorhanden ist, oder ein vorhandener, richtiger Wert.  
  
-   Nur Korrekturen, die auf der Wertebene, nicht auf der Datensatzebene, ausgeführt wurden, werden in die Wissensdatenbank importiert.  
  
-   Ungültige Werte werden erstellt, wenn der importierte Wert eine Domänenregel verletzt.  
  
-   Wenn Sie Werte aus mehreren Projekten gleichzeitig importieren, werden die Werte in sequenzieller Reihenfolge importiert.  
  
-   Eine Korrektur, die als Ergebnis einer begriffsbasierten Beziehung in einer Domäne vorgenommen wurde, wird als richtiger Wert (nicht als Fehler) importiert.  
  
##  <a name="ValuesNot"></a> Nicht importierte Werte  
 Die folgenden Werte werden nicht aus einem Projekt in eine Domäne importiert:  
  
-   Werte aus den Registerkarten **Vorgeschlagen** und **Ungültig** auf der Seite **Ergebnisse verwalten und anzeigen** der **Bereinigungsaktivität** werden nicht importiert.  
  
-   Wenn ein im Bereinigungsprojekt gefundener Wert einem vorhandenen Wert in der Domäne widerspricht, wird der im Projekt gefundene Wert übersprungen. Dies schließt Konflikte zwischen Bereinigungs- und Wissensdatenbankwerten ein.  
  
-   Korrekturen, die auf der Datensatzebene, ausgeführt wurden, werden nicht in die Wissensdatenbank importiert.  
  
-   Kein Wert wird in eine Domäne importiert, wenn der Wert, den er ersetzen würde, korrigiert oder von einem Verweisdatendienst als richtig angenommen wurde.  
  
-   Wenn ein Korrekturwert in der Wissensdatenbank als ungültig oder als Fehlerwert angezeigt wird, wird weder der Fehler noch der Korrekturwert importiert.  
  
-   Wenn die Domäne Teil einer Verbunddomäne ist und die Bereinigung in der Verbunddomäne ausgeführt wurde, werden keine Werte importiert.  
  
-   Sie können nur dann Werte aus einem Projekt importieren, wenn die Wissensdatenbank beschäftigt ist und vom importierenden Benutzer gesperrt wurde.  
  
## <a name="see-also"></a>Siehe auch  
 [Datenbereinigung](../data-quality-services/data-cleansing.md)   
 [DQS-Bereinigungstransformation](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)  
  
  
