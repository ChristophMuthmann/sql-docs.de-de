---
title: Erstellen eine Berichtsdatenquelle | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bd6662c7-ffbe-479d-8944-3dc858340998
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: b941dc8eb4fb1f0fc14d2565c8f1f65dd3ba4d15
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-report-data-source"></a>Erstellen einer Berichtsdatenquelle
  Damit Power View eine Verbindung mit einem mehrdimensionalen Modell herstellt, müssen Sie eine Datenquellendefinition für freigegebene Berichte, auch als RSDS-Datei bezeichnet, in einer SharePoint-Bibliothek erstellen. Die RSDS-Datei gibt den Namen einer Analysis Services-Serverinstanz, den Verbindungstyp, die Verbindungszeichenfolge und die Anmeldeinformationen an, die verwendet werden, um eine Verbindung mit einem mehrdimensionalen Modell herzustellen. Wenn ein Benutzer auf die RSDS-Datei klickt, wird ein neuer, leerer Power View-Bericht (eine RDLX-Datei) im Browser geöffnet.  
  
 Um eine RSDS-Verbindung zu erstellen, müssen SQL Server 2012 (oder höher) Reporting Services und das Reporting Services-Add-In für SharePoint 2010 oder SharePoint 2013 installiert sein.  
  
## <a name="create-a-report-data-source-rsds-connection-to-a-multidimensional-model"></a>Herstellen einer RSDS-Verbindung (Berichtsdatenquelle) mit einem mehrdimensionalen Modell  
 Bevor Sie beginnen, müssen Sie über folgende Informationen verfügen:  
  
-   Den Namen der Analysis Services-Serverinstanz, die im mehrdimensionalen Modus ausgeführt wird  
  
-   Den Namen der mehrdimensionalen Datenbank, mit der die Verbindung hergestellt werden soll  
  
-   Den Namen des Cubes, falls mehrere Cubes vorhanden sind  
  
-   (Optional) Den Perspektivennamen  
  
-   (Optional) Den Gebietsschemabezeichner  
  
#### <a name="to-create-a-shared-report-data-source-rsds-file-sharepoint-2010"></a>So erstellen Sie eine freigegebene Berichtsdaten-Quellendatei (RSDS-Datei) in Sharepoint 2010  
  
1.  Klicken Sie auf dem Bibliothekmenüband auf die Registerkarte **Dokumente** .  
  
2.  Klicken Sie auf **Neues Dokument**  > **Berichtsdatenquelle**.  
  
    > [!NOTE]  
    >  Wenn das Element **Berichtsdatenquelle** nicht im Menü angezeigt wird, wurde der Inhaltstyp für Berichtsdatenquellen noch nicht für diese Bibliothek aktiviert. Weitere Informationen finden Sie unter [Hinzufügen von Reporting Services-Inhaltstypen zu einer SharePoint-Bibliothek](../../reporting-services/report-server-sharepoint/add-reporting-services-content-types-to-a-sharepoint-library.md).  
  
3.  Klicken Sie auf der Seite **Datenquelleneigenschaften** auf **Name**, und geben Sie einen Namen für die RSDS-Verbindungsdatei ein.  
  
4.  Wählen Sie unter **Datenquellentyp**die Option **Microsoft BI-Semantikmodell für Power View**aus.  
  
5.  Geben Sie unter **Verbindungszeichenfolge**den Namen des Analysis Services-Servers, den Datenbanknamen, den Cubenamen sowie alle optionalen Einstellungen an.  
  
     Verbindungszeichenfolge: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’`  
  
    > [!NOTE]  
    >  Wenn mehrere Cubes vorhanden sind, müssen Sie einen Cubenamen angeben.  
  
     (Optional) Cubes können über Perspektiven verfügen, die den Benutzern eine Auswahlsicht bereitstellen, in der nur bestimmte Dimensionen und/oder Measuregruppen im Client sichtbar sind. Um eine Perspektive anzugeben, geben Sie den Perspektivennamen als Wert für die Cube-Eigenschaft ein: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<perspectivename>’`  
  
     (Optional) In Cubes können Metadaten und Datenübersetzungen für unterschiedliche Sprachen innerhalb des Modells angegeben werden. Damit die Übersetzungen (Daten und Metadaten) angezeigt werden, müssen Sie der Verbindungszeichenfolge die Locale Identifier-Eigenschaft hinzufügen: `Data source=<servername>;initial catalog=<multidimensionaldatabasename>-ee;cube='<cubename>’; Locale Identifier=<identifier number>`  
  
6.  Geben Sie in **Anmeldeinformationen**an, wie der Berichtsserver Anmeldeinformationen für den Zugriff auf die externe Datenquelle erhält.  
  
    -   Wählen Sie **Windows-Authentifizierung (integriert)** aus, wenn der Zugriff auf die Daten mit den Anmeldeinformationen des Benutzers erfolgen soll, der den Bericht geöffnet hat. Wählen Sie diese Option nicht aus, wenn für die SharePoint-Website oder -Farm die Formularauthentifizierung verwendet oder über ein vertrauenswürdiges Konto eine Verbindung mit dem Berichtsserver hergestellt wird. Wählen Sie diese Option nicht aus, wenn Sie eine Abonnement- oder Datenverarbeitung für diesen Bericht planen möchten. Diese Option kann am besten verwendet werden, wenn die Kerberos-Authentifizierung für die Domäne aktiviert ist oder wenn sich die Datenquelle auf demselben Computer wie der Berichtsserver befindet. Wenn die Kerberos-Authentifizierung nicht aktiviert ist, können die Windows-Anmeldeinformationen nur an einen anderen Computer weitergegeben werden. Dies bedeutet, dass statt der erwarteten Daten ein Fehler angezeigt wird, wenn sich die externe Datenquelle auf einem anderen Computer befindet, für den eine zusätzliche Verbindung erforderlich ist.  
  
    -   Wählen Sie **Zur Eingabe der Anmeldeinformationen auffordern** aus, wenn der Benutzer die Anmeldeinformationen bei jeder Ausführung des Berichts eingeben soll. Wählen Sie diese Option nicht aus, wenn Sie eine Abonnement- oder Datenverarbeitung für diesen Bericht planen möchten.  
  
    -   Wählen Sie **Gespeicherte Anmeldeinformationen** aus, wenn der Zugriff auf die Daten mit einem einzigen Satz Anmeldeinformationen erfolgen soll. Die Anmeldeinformationen werden vor der Speicherung verschlüsselt. Sie können Optionen auswählen, die bestimmen, wie die gespeicherten Anmeldeinformationen authentifiziert werden. Wählen Sie Windows-Anmeldeinformationen verwenden aus, wenn die gespeicherten Anmeldeinformationen zu einem Windows-Benutzerkonto gehören. Wählen Sie **Ausführungskontext für dieses Konto festlegen** aus, wenn Sie den Ausführungskontext auf dem Datenbankserver festlegen möchten.  
  
    -   Wählen Sie **Anmeldeinformationen sind nicht erforderlich** aus, wenn Sie Anmeldeinformationen in der Verbindungszeichenfolge angeben oder wenn Sie den Bericht mithilfe eines Kontos mit Minimalberechtigungen ausführen möchten.  
  
7.  Klicken Sie zum Testen auf **Verbindung testen** .  
  
8.  Wählen Sie **Diese Datenquelle aktivieren** aus, wenn die Datenquelle aktiviert sein soll. Wenn die Datenquelle konfiguriert, aber nicht aktiv ist, wird Benutzern beim Versuch, einen Bericht zu erstellen, eine Fehlermeldung angezeigt.  
  
  

