---
title: "Sicherheit (Berichts-Generator) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ed38291a-6afe-449f-9f32-3ae04502bd6f
caps.latest.revision: 11
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# Sicherheit (Berichts-Generator)
  Berichts-Generator ist eine für die Verwendung mit einem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Berichtsserver konzipierte Berichterstellungsclientanwendung. Der Berichtsserver kann im einheitlichen Modus als eigenständiger Server oder zur Unterstützung von Berichten auf einer SharePoint-Website im integrierten SharePoint-Modus konfiguriert werden.  
  
 Im Berichts-Generator können Sie Berichte, freigegebene Datasets und wiederverwendbare Berichtsteile erstellen. Auf einem Berichtsserver oder einer SharePoint-Website können Sie Berichte bearbeiten und freigegebene Datenquellen, freigegebene Datasets und freigegebene Berichtsteile hinzufügen.  
  
 Voraussetzung für die Erstellung, Veröffentlichung und Verwendung von Berichten und berichtsbezogenen Elementen ist ein Verständnis der Zusammenhänge zwischen Sicherheitsfunktionen und den folgenden Bereichen:  
  
-   **Berichtsserver oder SharePoint-Website, auf dem bzw. der Sie Berichte veröffentlichen:** Diese Funktionen werden vom Berichtsserveradministrator oder SharePoint-Websiteadministrator verwaltet.  
  
-   **Veröffentlichte Berichte und berichtsbezogene Elemente:** Zu den berichtsbezogenen Elementen zählen eingebettete und freigegebene Datenquellen und die zugehörigen Anmeldeinformationen, freigegebene Datasets, Parameter, Berichtsteile und Berichtsmodelle. Die Sicherheitsfunktionen für diese Elemente werden vom Autor des Berichts verwaltet. Der Berichtsserveradministrator bzw. SharePoint-Websiteadministrator muss dem Autor des Berichts ausreichende Berechtigungen gewähren, damit er die Elemente veröffentlichen und freigeben kann.  
  
-   **In einem Bericht verwendete externe Datenquellen:** Diese Funktionen werden vom Besitzer der externen Datenquelle verwaltet.  
  
-   **Auf externen Datenquellen basierende Berichtsmodelle:** Diese Funktionen werden vom Modell-Designer verwaltet.  
  
-   **Interaktive Berichtsfunktionen wie Parameter:** Diese Funktionen werden vom Autor des Berichts verwaltet.  
  
 In diesem Thema erfahren Sie, wie Sicherheitsfunktionen zum Verwalten und Schützen von Berichten und berichtsbezogenen Elementen verwendet werden.  
  
##  <a name="ReportServers"></a> Grundlegendes zur Sicherheit für Berichtsserver  
 Das Veröffentlichen und Anzeigen von Berichten sind privilegierte Vorgänge. Ein Berichtsserveradministrator stellt durch Berechtigungen sicher, dass nur autorisierte Benutzer Berichte auf den folgenden Berichtsservertypen veröffentlichen und anzeigen können:  
  
-   Im einheitlichen Modus konfigurierter Berichtsserver  
  
     Sie benötigen eine gültige URL und ausreichende Zugriffsberechtigungen für den Server, um eine Verbindung mit einem Berichtsserver herzustellen oder auf ihn zuzugreifen.  
  
     Für die Anzeige oder Veröffentlichung von Elementen auf einem Berichtsserver werden die für berichtsbezogene Elemente und Vorgänge geltenden Berechtigungssätze in Rollen organisiert. Ein Berichtsserveradministrator weist Sie einer oder mehreren Rollen zu. Die vordefinierte Rolle "Browser" ermöglicht Ihnen z. B. das Anzeigen von Berichten, Ordnern, Modellen und Ressourcen.  
  
     Wenden Sie sich an den Berichtsserveradministrator, wenn Sie keine Verbindung mit einem Berichtsserver herstellen können. Weitere Informationen finden Sie unter [Sicherheit und Schutz für Reporting Services](../../reporting-services/security/reporting-services-security-and-protection.md) in der Dokumentation zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312).  
  
-   Im integrierten SharePoint-Modus konfigurierter Berichtsserver  
  
     Sie benötigen eine gültige URL zur SharePoint-Website oder -Unterwebsite und ausreichende Berechtigungen, um eine Verbindung mit einer in einen Berichtsserver integrierten SharePoint-Website herzustellen.  
  
     Die Berechtigung für den Zugriff auf berichtsbezogene Elemente und Vorgänge wird mithilfe von SharePoint-Sicherheitsrichtlinien erteilt, durch die ein Benutzer- oder Gruppenkonto einer Berechtigungsebene für ein Element zugeordnet wird.  
  
     Wenden Sie sich an den SharePoint-Websiteadministrator, wenn Sie keine Verbindung mit einer SharePoint-Website herstellen können.  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="Reports"></a> Grundlegendes zur Sicherheit für veröffentlichte Berichte und berichtsbezogene Elemente  
 Die Sicherheit für Berichte und berichtsbezogene Elemente wird vom Berichtsserveradministrator verwaltet. Zu berichtsbezogenen Elementen zählen eingebettete und freigegebene Datenquellen sowie die zugehörigen Anmeldeinformationen, freigegebene Datasets, Parameter, Berichtsteile und Modelle.  
  
 Berichte und berichtsbezogene Elemente und Vorgänge können auf einem Berichtsserver oder einer SharePoint-Website unabhängig voneinander geschützt werden. Die Berechtigung für den Zugriff auf Elemente und Vorgänge wird mithilfe von Sicherheitsrichtlinien erteilt, durch die ein Benutzer- oder Gruppenkonto einer Berechtigungsebene für ein Element zugeordnet wird. Berechtigungen für einen Container, z. B. ein Ordner, werden von Elementen im Container geerbt, um die Komplexität und den Aufwand für die Verwaltung von Richtlinien zu reduzieren. Wenn ein Benutzer z. B. die spezifische Berechtigung "Berichte anzeigen" für einen Ordner besitzt, gilt diese Berechtigung für die Elemente im Ordner.  
  
 Berechtigungen für Elemente oder Ordner können mithilfe der Sicherheit auf Elementebene überschrieben werden. Wenn die Sicherheit auf Elementebene angewendet wird, gilt die Berechtigungsvererbung vom übergeordneten Container nicht mehr für das Element. Wird die Sicherheit auf Elementebene für einen Ordner angewendet, erben geschachtelte Ordner die gleichen Berechtigungen.  
  
 Falls Sie Elemente, die ein anderer Benutzer für Sie veröffentlicht hat, nicht finden oder auswählen können, liegt für das Element bzw. den Ordner möglicherweise ein Berechtigungsproblem vor.  
  
 Damit andere Benutzer von Ihnen veröffentlichte und freigegebene Elemente finden und auswählen können, müssen Sie vom Berichtsserveradministrator eine Ordnerorganisation einrichten lassen, die den jeweiligen Benutzern Zugriff bietet. Der Zugriff muss für das Erstellen von Berichten und Ausführen von veröffentlichten Berichten gewährt werden.  
  
 Weitere Informationen finden Sie in den folgenden Themen der Dokumentation zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Rollen und Berechtigungen &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  
-   [Verwalten von freigegebenen Datasets](../../reporting-services/report-data/manage-shared-datasets.md)  
  
### Updatebenachrichtigungen für Berichtsteile  
 Berichtsteile werden auf einem Berichtsserver veröffentlicht, damit sie für andere Benutzer freigegeben werden können. Beim Entwurf geben Sie den Speicherort an, an dem Berichtsteile veröffentlicht werden.  
  
 Benutzer, die Berichtsteile in ihre Berichte einschließen, können die Updatefunktion aktivieren. Wenn diese Funktion aktiviert ist, werden Benutzer über Änderungen von Berichtsteilen auf dem Berichtsserver benachrichtigt.  
  
 Wenn Berichtsteile vom ursprünglichen Speicherort verschoben werden, enthält die Updatebenachrichtigung sowohl den aktuellen als auch den vorherigen Speicherort des Berichtsteils. Akzeptieren Sie nur Updates von vertrauenswürdigen Speicherorten.  
  
 Weitere Informationen finden Sie unter [Berichtsteile &#40;Berichts-Generator und SSRS&#41;](../../reporting-services/report-design/report-parts-report-builder-and-ssrs.md).  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="Data"></a> Grundlegendes zur Sicherheit für Berichtsdaten und externe Datenquellen  
 Sie können in einem Bericht auf Daten aus externen Datenquellen zugreifen, indem Sie im Bericht eine eingebettete Datenquelle erstellen oder einen Verweis auf eine freigegebene Datenquelle oder ein freigegebenes Dataset hinzufügen.  
  
 Für jede externe Datenquelle müssen Sie Anmeldeinformationen mit entsprechenden Berechtigungen für den Zugriff auf die Quelle und die zugrunde liegenden Daten angeben. Der Datenquellenbesitzer gibt den erforderlichen Anmeldeinformationstyp für diesen Zugriff an.  
  
 Anmeldeinformationen werden nicht in der Berichtsdefinition gespeichert. Sie werden unabhängig vom Bericht auf dem Berichtsserver oder der SharePoint-Website und im Berichterstellungsclient verwaltet.  
  
 Beim Entwerfen des Berichts werden Anmeldeinformationen verwendet, um Datasetabfragen auszuführen und den Bericht in der Vorschau anzuzeigen. Zur Laufzeit werden Anmeldeinformationen verwendet, um den Bericht auszuführen und Abfrageergebnisse zwischenzuspeichern. Die Abfrageergebnisse für ein freigegebenes Dataset können auch unabhängig zwischengespeichert werden. Die Entwurfszeit- und Laufzeitanmeldeinformationen können sich unterscheiden. Weitere Informationen finden Sie unter [Angeben von Anmeldeinformationen im Berichts-Generator](../Topic/Specify%20Credentials%20in%20Report%20Builder.md).  
  
 Weitere Informationen zum Schützen von Daten finden Sie in den folgenden Themen der Dokumentation zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312):  
  
-   [Sicherheitscenter für SQL Server-Datenbankmodul und Azure SQL-Datenbank](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
 Weitere Informationen zu Datenquellen finden Sie unter [Datenverbindungen, Datenquellen und Verbindungszeichenfolgen in Berichts-Generator](../Topic/Data%20Connections,%20Data%20Sources,%20and%20Connection%20Strings%20in%20Report%20Builder.md).  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="Models"></a> Grundlegendes zu Modellen und Sicherheitsfiltern  
 Wenn Daten aus einem auf externen Daten basierenden Berichtsmodell abgerufen werden, können Sie im Modell Sicherheitsfilter anwenden. So können Daten gut geschützt werden, da jeder Benutzer, der einen Bericht ausführt, nur die Daten sieht, für die er über Berechtigungen verfügt.  
  
 Berichtsparameter werden nicht für die Sicherheit auf Zeilenebene verwendet. Sie verhindern nicht, dass Benutzer oder Benutzergruppen bestimmte Datenzeilen sehen. Die Sicherheit der im Bericht angezeigten Daten muss mit Sicherheitsfiltern oder der Modellelementsicherheit gewährleistet werden.  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
##  <a name="Interactive"></a> Grundlegendes zur Sicherheit der Berichterstellung für interaktive Funktionen  
 In Berichten werden häufig Parameter verwendet, um Benutzern die interaktive Anpassung ihrer Ansicht eines Berichts zu ermöglichen. Die folgenden bewährten Tipps helfen Ihnen, gut durchdachte Berichte zu erstellen:  
  
-   Verwenden Sie Parameter, die auf Abfrageparametern basieren und vom Typ **Text** sind, nur, wenn Sie gültige Werte geben. Durch eine Liste verfügbarer Werte stellen Sie sicher, dass Benutzer nur gültige Werte auswählen. Ohne eine solche Liste ist es nicht möglich, die Werte einzuschränken, die ein Benutzer eingeben kann.  
  
-   Verwenden Sie nicht die globale [UserID] zum Schützen privater Daten. Dieser Wert kann anhand der URL-Zugriffssyntax als Berichtsparameter in einer Berichts-URL angegeben werden. Wird dieser Wert in einem Ausdruck in einem freigegebenen Dataset verwendet, kann das Dataset nicht zwischengespeichert werden. Weitere Informationen finden Sie unter [URL-Zugriffsparameterverweis](../../reporting-services/url-access-parameter-reference.md) in der Dokumentation zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 Auf einem Berichtsserver veröffentlichte Elemente können vom Berichtsserveradministrator mithilfe der rollenbasierten Sicherheit oder der Sicherheit auf Ordner- und Elementebene geschützt werden. Weitere Informationen finden Sie unter [Sichere Berichte und Ressourcen](../../reporting-services/security/secure-reports-and-resources.md) in der Dokumentation zu [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-[Onlinedokumentation](http://go.microsoft.com/fwlink/?linkid=121312).  
  
 ![Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird](../../analysis-services/instances/media/uparrow16x16.png "Pfeilsymbol, dass mit dem Link "Zurück zum Anfang" verwendet wird") [Zurück zum Anfang](#BackToTop)  
  
## Siehe auch  
 [Installieren und Deinstallieren von Berichts-Generator](../Topic/Install%20and%20Uninstall%20Report%20Builder.md)   
 [Berichtsparameter &#40;Berichts-Generator und Berichts-Designer&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)  
  
  