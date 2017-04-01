---
title: "Datenprofil-Viewer | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Datenprofil-Viewer [Integration Services]"
  - "Datenprofilerstellungs-Task [Integration Services], Ausgabe-Viewer"
ms.assetid: b9043428-ce26-45bb-910c-588d07579565
caps.latest.revision: 26
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 26
---
# Datenprofil-Viewer
  Das Anzeigen und Analysieren der Datenprofile ist der nächste Schritt bei der Datenprofilerstellung. Sie können diese Profile anzeigen, nachdem Sie den Datenprofilerstellungs-Task innerhalb eines [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Pakets ausgeführt und die Datenprofile berechnet haben. Weitere Informationen zum Verwenden und Einrichten und Ausführen der Datenprofilerstellungs-Tasks finden Sie unter [Einrichten von Datenprofilerstellungs-Tasks](../../integration-services/control-flow/setup-of-the-data-profiling-task.md).  
  
> [!IMPORTANT]  
>  Die Ausgabedatei enthält möglicherweise vertrauliche Daten über Ihre Datenbank und die darin enthaltenen Daten. Vorschläge zur Verbesserung der Sicherheit dieser Datei finden Sie unter [Zugriff auf Dateien, die von Paketen verwendet werden](../../integration-services/security/access-to-files-used-by-packages.md).  
  
## Datenprofile  
 Wenn Sie die Datenprofile anzeigen möchten, konfigurieren Sie den Datenprofilerstellungs-Task so, dass dieser seine Ausgabe an eine Datei sendet, und verwenden Sie dann den eigenständigen Datenprofil-Viewer. Gehen Sie folgendermaßen vor, um den Datenprofil-Viewer zu öffnen.  
  
-   Klicken Sie mit der rechten Maustaste im **-Designer auf den Task **Datenprofilerstellung[!INCLUDE[ssIS](../../includes/ssis-md.md)], und klicken Sie dann auf **Bearbeiten**. Klicken Sie auf der Seite **Allgemein** des **Editors für den Datenprofilerstellungs-Task** auf **Profil-Viewer öffnen**.  
  
-   Führen Sie im Ordner „*\<Laufwerk>*:\Program Files (x86) | Program Files\Microsoft SQL Server\110\DTS\Binn“ die Datei „DataProfileViewer.exe“ aus.  
  
 Der Viewer verwendet mehrere Bereiche, um die von Ihnen angeforderten Profile und berechneten Ergebnisse mit optionaler Detail- und Drilldownfunktion anzuzeigen.  
  
 Bereich **Profile**  
 Der Bereich **Profile** zeigt die Profile an, die im Datenprofil-Task angefordert wurden. Wenn Sie die für das Profil berechneten Ergebnisse anzeigen möchten, wählen Sie im Bereich **Profile** das Profil aus. Die Ergebnisse werden dann in den anderen Bereichen des Viewers angezeigt.  
  
 Bereich**Ergebnisse**   
 Der Bereich **Ergebnisse** verwendet eine einzelne Zeile, um die berechneten Ergebnisse des Profils zusammenzufassen. Wenn Sie beispielsweise ein **Verteilungsprofil für Spaltenlänge**anfordern, enthält diese Zeile die minimale und maximale Länge und die Zeilenanzahl. Für die meisten Profile können Sie diese Zeile im Bereich **Ergebnisse** auswählen, um zusätzliche Details im optionalen Bereich **Details** anzuzeigen.  
  
 Bereich **Details**  
 Für die meisten Profiltypen zeigt der Bereich **Details** zusätzliche Informationen zu den Profilergebnissen an, die im Bereich **Ergebnisse** ausgewählt wurden. Wenn Sie beispielsweise ein **Verteilungsprofil für Spaltenlänge**anfordern, zeigt der Bereich **Details** jede gefundene Spaltenlänge an. Der Bereich zeigt auch die Anzahl und den Prozentwert der Zeilen an, in denen der Spaltenwert diese Spaltenlänge hat.  
  
 Für die drei Profiltypen, die für mehrere Spalten berechnet werden (Kandidatenschlüssel, funktionale Abhängigkeit und Wertinklusion), zeigt der Bereich **Details** Verletzungen der erwarteten Beziehung an. Wenn Sie beispielsweise ein Kandidatenschlüsselprofil anfordern, zeigt der Detailbereich doppelte Werte an, die die Eindeutigkeit des Kandidatenschlüssels verletzen.  
  
 Wenn die Datenquelle verfügbar ist, mit der das Profil berechnet wird, können Sie im Bereich **Details** auf eine Zeile doppelklicken, um die übereinstimmenden Datenzeilen im Bereich **Drilldown** anzuzeigen.  
  
 Bereich **Drilldown**  
 Sie können im Bereich **Details** auf eine Zeile doppelklicken, um die übereinstimmenden Datenzeilen im Bereich **Drilldown** anzuzeigen, wenn die folgenden Bedingungen erfüllt sind:  
  
-   Die Datenquelle, mit der das Profil berechnet wird, ist verfügbar.  
  
-   Sie sind berechtigt, die Daten anzuzeigen.  
  
 Um für eine Drilldownanforderung eine Verbindung mit der Quelldatenbank herzustellen, verwendet der Datenprofil-Viewer die Windows-Authentifizierung und die Anmeldeinformationen des aktuellen Benutzers. Der Datenprofil-Viewer verwendet nicht die Verbindungsinformationen, die im Paket gespeichert sind, das den Datenprofilerstellungs-Task ausgeführt hat.  
  
> [!IMPORTANT]  
>  Die Drilldownfunktion, die im Datenprofil-Viewer verfügbar ist, sendet Live-Abfragen an die ursprüngliche Datenquelle. Diese Abfragen haben möglicherweise negative Auswirkungen auf die Leistung des Servers.  
>   
>  Wenn Sie einen Drilldown für eine Ausgabedatei ausführen, die nicht vor kurzem erstellt wurde, geben die Drilldownabfragen möglicherweise nicht die Gruppe von Zeilen zurück, mit denen die ursprüngliche Ausgabe berechnet wurde.  
  
 Weitere Informationen zur Benutzeroberfläche des Datenprofil-Viewers finden Sie unter [Data Profile Viewer F1 Help](../../integration-services/control-flow/data-profile-viewer-f1-help.md).  
  
  