---
title: "Verarbeiten von große Berichten | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- report processing [Reporting Services], large reports
- page breaks [Reporting Services]
- large reports
- size [SQL Server], reports
- distributing reports [Reporting Services], large reports
ms.assetid: c5275a9f-c95b-46d7-bc62-633879a8a291
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 065902778339650fcd123556acdeabfe8504224f
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="process-large-reports"></a>Verarbeiten von großen Berichten
  Die Verarbeitung umfangreicher Berichte stellt eine Herausforderung dar und erfordert bestimmte Konfigurationseinstellungen, damit die Berichte ordnungsgemäß ausgeführt werden können. Sie sollten nur dann bedarfsgesteuert ausgeführt werden, wenn sie die Paginierung unterstützen.  
  
> [!NOTE]  
>  Seitenumbrüche sind standardmäßig aktiviert. Sie sollten sie nicht deaktivieren, wenn Sie davon ausgehen, dass der Bericht große Datenmengen enthält. Im HTML-Renderingformat, mit dem ein Bericht zunächst gerendert wird, werden Berichte in einem Browser geöffnet. Bei Berichten ohne Paginierung sind alle Daten auf einer einzigen Seite enthalten, was nur wenige Browser unterstützen. Beispielsweise kann ein Bericht mit 5.000 Datenzeilen mit Sicherheit nicht auf einer einzigen Seite in einem Browser angezeigt werden.  
  
 Wenn Sie mit einem umfangreichen Bericht arbeiten, müssen die von Ihnen ausgewählten Optionen für Berichtsausführung, Rendering und Übermittlung für große Dokumente geeignet sein. Die Größe eines Berichts wird weitgehend von dem durch die Abfrage zurückgegebenen Rowset sowie von der zur Anzeige des Berichts verwendeten Renderingerweiterung bestimmt.  
  
 Bei Berichten, die flüchtige Daten enthalten, kann die Berichtsgröße von Bericht zu Bericht erheblich variieren. In diesem Fall sollten Sie die Datenquelle überwachen, um zu bestimmen, welche Auswirkungen die Flüchtigkeit der Daten auf Ihren Bericht hat und ob Sie sich an die in diesem Abschnitt beschriebenen Schritte halten müssen.  
  
 Weitere Informationen und Tipps für die Diagnose von Timeoutfehlern und Fehlern aufgrund von unzureichendem Speicher finden Sie im Artikel [How to diagnose issues when running reports in the report server](http://go.microsoft.com/fwlink/?LinkId=85634) (Gewusst wie: Diagnose von Problemen bei der Ausführung von Berichten im Berichtsserver) unter blogs.msdn.com.  
  
## <a name="configuration-recommendations"></a>Konfigurationsempfehlungen  
 Für das Ausführen und Rendern von Berichten sowie für den Zugriff auf Berichte gelten die folgenden Empfehlungen:  
  
-   Entwerfen Sie den Bericht so, dass die Paginierung unterstützt wird. Der Berichtsserver sendet einen Bericht seitenweise. Bei einem Bericht mit Paginierung können Sie steuern, wie viele Daten an den Browser gesendet werden. Weitere Informationen finden Sie unter [Vorabladen des Caches &#40;Berichts-Manager&#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md).  
  
-   Konfigurieren Sie den Bericht so, dass er als geplante Berichtsmomentaufnahme ausgeführt wird, um eine bedarfsgesteuerte Ausführung zu verhindern. Legen Sie keinen Timeoutwert für die Berichtsausführung fest. Führen Sie den Bericht außerhalb der Spitzenzeiten aus.  
  
-   Konfigurieren Sie den Bericht so, dass eine freigegebene Datenquelle verwendet wird, falls Sie selbst entscheiden möchten, ob der Bericht verarbeitet wird. Das Verwenden einer freigegebenen Datenquelle bietet den Vorteil, dass diese Option deaktiviert werden kann. Die Deaktivierung der Datenquelle verhindert die Verarbeitung des Berichts.  
  
-   Deaktivieren Sie den Berichtsverlauf, wenn Sie Speicherplatz freigeben möchten. Zum Deaktivieren des Berichtsverlaufs deaktivieren Sie alle Kontrollkästchen auf der Eigenschaftenseite Verlauf.  
  
-   Beschränken Sie den Zugriff auf den Bericht. Konfigurieren Sie die Verwendung der Sicherheit auf Elementebene für den Bericht und ersetzen Sie die Standardrollenzuweisungen durch neue Rollenzuweisungen, die nur den Benutzern Zugriff gewähren, die den Bericht benötigen.  
  
     Standardmäßig können Benutzer einen beliebigen Bericht öffnen, den sie in der Ordnerhierarchie anzeigen können. Selbst wenn Sie für einen Bericht die Ausführung als Momentaufnahme konfigurieren, können Benutzer, die das Berichtselement in einem Ordner anzeigen können, den Bericht öffnen. Bei einem sehr umfangreichen Bericht kann es passieren, dass der Browser nicht mehr reagiert, wenn ein Benutzer den Bericht im Berichts-Manager öffnet.  
  
## <a name="rendering-recommendations"></a>Renderingempfehlungen  
 Vor der Konfiguration der Berichtsverteilung müssen Sie unbedingt wissen, welche Renderingclients für umfangreiche Dokumente ausgelegt sind. Als Format wird die standardmäßige HTML-Renderingerweiterung mit weichen Seitenumbrüchen empfohlen, Sie können aber jedes Format auswählen, das die Paginierung unterstützt.  
  
 Jedes Renderingformat besitzt eine andere Leistung und Arbeitsspeicherverwendung. Ein Bericht wird abhängig vom ausgewählten Format unterschiedlich schnell ausgegeben und benötigt unterschiedlichen Speicherplatz. Zu den schnellsten und am wenigsten arbeitsspeicherintensiven Formaten zählen CSV, XML und HTML. PDF und Excel zeigen die schwächste Leistung, jedoch aus anderen Gründen. PDF ist CPU-intensiv, während Excel RAM-intensiv ist. Bildrendering fällt zwischen diese beiden Gruppen. Das Format können Sie beim Definieren der Methode zum Verteilen des Berichts angeben.  
  
## <a name="deployment-and-distribution-recommendations"></a>Empfehlungen zur Bereitstellung und Verteilung  
 Wenn Sie zum Steuern des Renderns von Berichten Seitenumbrüche verwenden, können Sie einen sehr umfangreichen Bericht auf die gleiche Weise bereitstellen wie jeden anderen Bericht. Zugriff auf den Bericht ermöglichen Sie über den Berichts-Manager, ein SharePoint-Webpart oder eine URL, die Sie zu einem Portal oder zu einer Website hinzufügen. Sämtliche Bereitstellungsoptionen unterstützen den bedarfsgesteuerten Zugriff sowie eine zuvor ausgeführte Berichtsmomentaufnahme.  
  
 Eine alternative Bereitstellungsstrategie stellt das Verteilen von Berichten an einzelne Benutzer dar. Wenn Sie die Übermittlungsoptionen sorgfältig konfigurieren, können Sie umfangreiche Berichte mithilfe von Abonnements verteilen. Sie können entweder ein Standardabonnement oder ein datengesteuertes Abonnement zum Übermitteln des Berichts verwenden. Es folgen Empfehlungen zum Abonnieren und Übermitteln:  
  
-   Konfigurieren Sie ein Abonnement so, dass Webarchiv (MHTML), PDF oder Excel verwendet wird.  
  
-   Konfigurieren Sie die Dateifreigabeübermittlung für ein Abonnement, wenn Sie PDF oder Excel verwenden. Nach Übermittlung des Berichts können Sie ihn mit einer Desktopanwendung verwenden. Legen Sie Berechtigungen für die Dateifreigabe fest, um zu bestimmen, wer den Bericht anzeigen kann.  
  
     Beachten Sie, dass ein Bericht in der Dateifreigabe nicht mehr durch [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]kontrolliert oder gesichert wird. Wenn Sie bei einem Update des Berichts benachrichtigt werden möchten, erstellen Sie ein zweites Abonnement, das die E-Mail-Übermittlung nur zum Senden einer Benachrichtigung verwendet.  
  
 Für eine Übermittlung von Berichten per E-Mail müssen Sie das Abonnement so konfigurieren, dass es einen Link einschließt. Sie sollten Berichte nicht als Anlage versenden.  
  
## <a name="see-also"></a>Siehe auch  
 [Abonnements und Übermittlung &#40;Reporting Services&#41;](../../reporting-services/subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Festlegen von Berichtsverarbeitungseigenschaften](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Angeben der Anmeldeinformationen und Verbindungsinformationen für Berichtsdatenquellen-Verbindungen](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Berichtsinhaltsverwaltung für Server &#40; SSRS im einheitlichen Modus &#41;](../../reporting-services/report-server/report-server-content-management-ssrs-native-mode.md)   
 [Vorabladen des Caches &#40; Berichts-Manager &#41;](../../reporting-services/report-server/preload-the-cache-report-manager.md)  
  
  

