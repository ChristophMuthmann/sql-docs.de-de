---
title: "Importieren aus einem Datenfeed (SSAS – tabellarisch) | Microsoft Docs"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
caps.latest.revision: 15
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 643286048299d79c504bd3e6c80e63e23aef6563
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="import-data---data-feed"></a>Importieren von Daten - Datenfeed
  Datenfeeds sind einzelne oder mehrere XML-Datenströme, die von einer Onlinedatenquelle generiert und in ein Zieldokument oder eine Zielanwendung gestreamt werden. Mit dem Tabellenimport-Assistenten können Sie Daten aus einem Datenfeed in Ihr Modell importieren.  
  
 Dieses Thema enthält folgende Abschnitte:  
  
-   [Grundlegendes zum Importieren aus einem Datenfeed](#prereq)  
  
-   [Importieren von Daten aus einem Azure DataMarket-Dataset](#azure)  
  
-   [Importieren von Datenfeeds aus öffentlichen oder Unternehmensdatenquellen](#importdata)  
  
-   [Importieren von Datenfeeds aus SharePoint-Listen](#importlist)  
  
-   [Importieren von Datenfeeds aus Reporting Services-Berichten](#importreport)  
  
##  <a name="prereq"></a> Grundlegendes zum Importieren aus einem Datenfeed  
 Sie können Daten aus den folgenden Arten von Datenfeeds in ein tabellarisches Modell importieren:  
  
 **Reporting Services-Bericht**  
 Sie können auf einer SharePoint-Website oder einem Berichtsserver veröffentlichte Reporting Services-Berichte als Datenquelle in einem Modell verwenden. Beim Importieren von Daten aus einem Reporting Services-Bericht müssen Sie eine Berichtsdefinitionsdatei (.rdl) als Datenquelle angeben.  
  
 **Azure DataMarket-Dataset**  
 Azure DataMarket ist ein Dienst, der im Rahmen von Clouddiensten einen Marketplace und einen Übermittlungskanal für Informationen bereitstellt. Azure DataMarket-Datasets erfordern anstelle eines Windows-Benutzerkontos einen Kontoschlüssel.  
  
 **Atom-Feeds**  
 Beim Feed muss es sich um einen Atom-Feed handeln. RSS-Feeds werden nicht unterstützt. Der Feed muss entweder öffentlich verfügbar sein, oder Sie müssen über die Berechtigung verfügen, unter dem angemeldeten Windows-Konto eine Verbindung mit dem Feed herzustellen.  
  
 Daten aus einem Datenfeed werden einem Modell während des Imports einmal hinzugefügt. Um aktualisierte Daten aus dem Feed zu erhalten, können Sie entweder die Daten aus dem Modell-Designer aktualisieren oder einen Datenaktualisierungszeitplan für das Modell konfigurieren, nachdem es auf einer Produktionsinstanz von Analysis Services bereitgestellt wurde. Weitere Informationen finden Sie unter [Verarbeiten von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="azure"></a> Importieren von Daten aus einem Azure DataMarket-Dataset  
 Sie können Daten aus einem Azure DataMarket als Tabelle in Ihr Modell importieren.  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>So importieren Sie Daten aus einem Azure DataMarket-Dataset  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Aus Datenquelle importieren**. Der Tabellenimport-Assistent wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Mit einer Datenquelle verbinden** unter **Datenfeeds**die Option **Azure DataMarket-Dataset**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Verbindung mit einem Azure DataMarket-Dataset herstellen** unter **Anzeigename**einen aussagekräftigen Namen für den Feed ein, auf den Sie zugreifen. Beim Importieren mehrerer Feeds oder Datenquellen können aussagekräftige Verbindungsnamen Informationen bereitstellen, wie die Verbindung verwendet wird.  
  
4.  Geben Sie unter **Datenfeed-URL**die Adresse für den Datenfeed ein.  
  
5.  Geben Sie in **Sicherheitseinstellungen**unter **Kontoschlüssel**einen Kontoschlüssel ein. Kontoschlüssel werden von Analysis Services für den Zugriff auf DataMarket-Abonnements verwendet.  
  
6.  Klicken Sie auf **Verbindung testen** , um sicherzustellen, dass der Feed verfügbar ist. Sie können auch auf **Erweitert** klicken, um zu bestätigen, dass die Basis- oder Dienstdokument-URL die Abfrage oder das Dienstdokument mit dem Feed enthält.  
  
7.  Klicken Sie auf **Weiter** , um den Import fortzusetzen.  
  
8.  Geben Sie auf der Seite **Identitätswechselinformationen** die Anmeldeinformationen an, die von Analysis Services verwendet werden, um beim Aktualisieren der Daten eine Verbindung mit der Datenquelle herzustellen, und klicken Sie dann auf **Weiter**. Diese Anmeldeinformationen unterscheiden sich vom Kontoschlüssel.  
  
9. Geben Sie im Assistenten auf der Seite **Tabellen und Sichten auswählen** im Feld **Anzeigename** einen aussagekräftigen Namen ein, durch den die Tabelle identifiziert wird, in der die Daten nach dem Import enthalten sind.  
  
10. Klicken Sie auf **Vorschau anzeigen und filtern** , um die Daten zu überprüfen und die Spaltenauswahl zu ändern. Sie können die Zeilen, die in den Berichtsdatenfeed importiert werden, nicht einschränken. Sie können jedoch Spalten entfernen, indem Sie die entsprechenden Kontrollkästchen deaktivieren. Klicken Sie auf **OK**.  
  
11. Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
##  <a name="importdata"></a> Importieren von Datenfeeds aus öffentlichen oder Unternehmensdatenquellen  
 Sie können auf öffentliche Feeds zugreifen oder benutzerdefinierte Datendienste erstellen, die Atom-Feeds aus proprietären oder Legacydatenbanksystemen generieren.  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>So importieren Sie Daten aus öffentlichen oder Unternehmensdatenfeeds  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Aus Datenquelle importieren**. Der Tabellenimport-Assistent wird geöffnet.  
  
2.  Wählen Sie auf der Seite **Mit einer Datenquelle verbinden** unter **Datenfeeds**die Option **Andere Feeds**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Mit einem Datenfeed verbinden** einen aussagekräftigen Namen für den Feed ein, auf den Sie zugreifen. Beim Importieren mehrerer Feeds oder Datenquellen können aussagekräftige Verbindungsnamen Informationen bereitstellen, wie die Verbindung verwendet wird.  
  
4.  Geben Sie unter **Datenfeed-URL**die Adresse für den Datenfeed ein. Gültige Werte sind:  
  
    1.  Ein XML-Dokument, das die Atom-Daten enthält. Die folgende URL zeigt z. B. auf einen öffentlichen Feed der Open Government Data Initiative-Website:  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  Ein ATOMSVC-Dokument, das einen oder mehrere Feeds angibt. ATOMSVC-Dokumente zeigen auf Dienste oder Anwendungen, die einen oder mehrere Feeds bereitstellen. Die einzelnen Feeds werden als Basisabfragen angegeben, die das Resultset zurückgeben.  
  
         Sie können eine URL-Adresse zu einem ATOMSVC-Dokument angeben, das sich auf einem Webserver befindet, oder die Datei in einem freigegebenen oder lokalen Ordner auf Ihrem Computer öffnen. Sie verfügen über ein ATOMSVC-Dokument, wenn dieses beim Exportieren eines Reporting Services-Berichts auf dem Computer gespeichert wurde. ATOMSVC-Dokumente können sich zudem in Datenfeedbibliotheken befinden, die ein Benutzer für die SharePoint-Website erstellt hat.  
  
        > [!NOTE]  
        >  Es wird empfohlen, ein ATOMSVC-Dokument anzugeben, auf das über eine URL-Adresse oder einen freigegebenen Ordner zugegriffen werden kann, da auf diese Weise nach der Veröffentlichung der Arbeitsmappe in SharePoint automatische Datenaktualisierungen für die Arbeitsmappe konfiguriert werden können. Auf dem Server können dieselben URL-Adressen oder Netzwerkordner für die Datenaktualisierung verwendet werden, wenn Sie auf dem Computer keinen lokalen Speicherort angeben.  
  
5.  Klicken Sie auf **Verbindung testen** , um sicherzustellen, dass der Feed verfügbar ist. Sie können auch auf **Erweitert** klicken, um zu bestätigen, dass die Basis- oder Dienstdokument-URL die Abfrage oder das Dienstdokument mit dem Feed enthält.  
  
6.  Klicken Sie auf **Weiter** , um den Import fortzusetzen.  
  
7.  Geben Sie auf der Seite **Identitätswechselinformationen** die Anmeldeinformationen an, die von Analysis Services verwendet werden, um beim Aktualisieren der Daten eine Verbindung mit der Datenquelle herzustellen, und klicken Sie dann auf **Weiter**.  
  
8.  Ersetzen Sie im Assistenten auf der Seite **Tabellen und Sichten auswählen** im Feld **Anzeigename** den Datenfeedinhalt durch einen aussagekräftigen Namen, der die Tabelle identifiziert, die die Daten nach dem Import enthalten soll.  
  
9. Klicken Sie auf **Vorschau anzeigen und filtern** , um die Daten zu überprüfen und die Spaltenauswahl zu ändern. Sie können die Zeilen, die in den Berichtsdatenfeed importiert werden, nicht einschränken. Sie können jedoch Spalten entfernen, indem Sie die entsprechenden Kontrollkästchen deaktivieren. Klicken Sie auf **OK**.  
  
10. Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
##  <a name="importlist"></a> Importieren von Datenfeeds aus SharePoint-Listen  
 Es können alle SharePoint-Listen importiert werden, für die im Menüband (SharePoint) die Schaltfläche **Als Datenfeed exportieren** angezeigt wird. Sie können auf diese Schaltfläche klicken, um die Liste als Feed zu exportieren.  
  
> [!NOTE]  
>  Dies gilt nur für SharePoint 2010 und SharePoint 2013.  
   
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>So importieren Sie Datenfeeds aus einer SharePoint-Liste  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Aus Datenquelle importieren**.  
  
2.  Wählen Sie auf der Seite **Mit einer Datenquelle verbinden** unter **Datenfeeds**die Option **Andere Datenfeeds**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite **Mit einem Datenfeed verbinden** einen aussagekräftigen Namen für den Feed ein, auf den Sie zugreifen. Beim Importieren mehrerer Feeds oder Datenquellen können aussagekräftige Verbindungsnamen Informationen bereitstellen, wie die Verbindung verwendet wird.  
  
4.  Geben Sie in Datenfeed-URL eine Adresse zum listendatendienst, und Ersetzen Sie dabei \<Server-Name > durch den tatsächlichen Namen Ihres SharePoint-Servers:  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  Klicken Sie auf **Verbindung testen** , um sicherzustellen, dass der Feed verfügbar ist. Sie können auch auf **Erweitert** klicken, um zu bestätigen, dass die Dienstdokument-URL eine Adresse zum Listendatendienst enthält.  
  
6.  Klicken Sie auf **Weiter** , um den Import fortzusetzen.  
  
7.  Geben Sie auf der Seite **Identitätswechselinformationen** die Anmeldeinformationen an, die von Analysis Services verwendet werden, um beim Aktualisieren der Daten eine Verbindung mit der Datenquelle herzustellen, und klicken Sie dann auf **Weiter**.  
  
8.  Wählen Sie im Assistenten auf der Seite **Tabellen und Sichten auswählen** die zu importierenden Listen aus.  
  
    > [!NOTE]  
    >  Sie können nur Listen importieren, die Spalten enthalten.  
  
9. Klicken Sie auf **Vorschau anzeigen und filtern** , um die Daten zu überprüfen und die Spaltenauswahl zu ändern. Sie können die Zeilen, die in den Berichtsdatenfeed importiert werden, nicht einschränken. Sie können jedoch Spalten entfernen, indem Sie die entsprechenden Kontrollkästchen deaktivieren. Klicken Sie auf **OK**.  
  
10. Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
##  <a name="importreport"></a> Importieren von Datenfeeds aus Reporting Services-Berichten  
 Wenn Sie über eine [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] Reporting Services-Bereitstellung verfügen, können Sie einen Datenfeed mithilfe der Atom-Renderingerweiterung aus einem vorhandenen Bericht generieren.  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>So importieren Sie Berichtsdaten aus einem veröffentlichten Reporting Services-Bericht  
  
1.  Klicken Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]auf das Menü **Modell** und dann auf **Aus Datenquelle importieren**.  
  
2.  Wählen Sie auf der Seite **Mit einer Datenquelle verbinden** unter **Datenfeeds**die Option **Bericht**aus, und klicken Sie dann auf **Weiter**.  
  
3.  Geben Sie auf der Seite Verbindung mit einem Microsoft SQL Server Reporting Services-Bericht herstellen unter Anzeigename der Verbindung einen aussagekräftigen Namen für den Feed ein, auf den Sie zugreifen. Beim Importieren mehrerer Datenquellen können aussagekräftige Verbindungsnamen Informationen bereitstellen, wie die Verbindung verwendet wird.  
  
4.  Klicken Sie auf **Durchsuchen** , und wählen Sie einen Berichtsserver aus.  
  
     Wenn Sie regelmäßig Berichte auf einem Berichtsserver verwenden, wird der Server möglicherweise in der Liste **Letzte Sites und Server**aufgeführt. Geben Sie andernfalls unter Name eine Adresse zu einem Berichtsserver ein, und klicken Sie auf **Öffnen** , um die Ordner auf der Berichtsserver-Website zu durchsuchen. Eine Beispieladresse für einen Berichtsserver möglicherweise http://\<Computername > / Reportserver.  
  
5.  Wählen Sie den Bericht aus, und klicken Sie auf **Öffnen**. Sie können auch im Textfeld **Name** einen Link einschließlich des vollständigen Pfads und Berichtsnamens zum Bericht einfügen. Der Tabellenimport-Assistent stellt eine Verbindung mit dem Bericht her und rendert ihn im Vorschaubereich.  
  
     Wenn im Bericht Parameter verwendet werden, müssen Sie einen Parameter angeben. Andernfalls können Sie keine Berichtsverbindung erstellen. In diesem Fall werden nur die Zeilen, die mit dem Parameterwert verknüpft sind, in den Datenfeed importiert.  
  
    1.  Wählen Sie im Listenfeld oder Kombinationsfeld des Berichts einen Parameter aus.  
  
    2.  Klicken Sie auf **Bericht anzeigen** , um die Daten zu aktualisieren.  
  
        > [!NOTE]  
        >  Wenn Sie den Bericht anzeigen, werden die ausgewählten Parameter zusammen mit der Datenfeeddefinition gespeichert.  
  
     Sie können auch auf **Erweitert** klicken, um anbieterspezifische Eigenschaften für den Bericht festzulegen.  
  
6.  Klicken Sie auf **Verbindung testen** , um sicherzustellen, dass der Bericht als Datenfeed verfügbar ist. Sie können auch auf **Erweitert** klicken, um zu bestätigen, dass die Eigenschaft **Inlinedienstdokument** eingebettetes XML enthält, das die Datenfeedverbindung angibt.  
  
7.  Klicken Sie auf **Weiter** , um den Import fortzusetzen.  
  
8.  Geben Sie auf der Seite **Identitätswechselinformationen** die Anmeldeinformationen an, die von Analysis Services verwendet werden, um beim Aktualisieren der Daten eine Verbindung mit der Datenquelle herzustellen, und klicken Sie dann auf **Weiter**.  
  
9. Aktivieren Sie auf der Seite **Tabellen und Sichten auswählen** des Assistenten das Kontrollkästchen neben den Berichtsteilen, die Sie als Daten importieren möchten.  
  
     Einige Berichte können mehrere Teile enthalten, einschließlich Tabellen, Listen oder Diagramme.  
  
10. Geben Sie im Feld **Anzeigename** den Namen der Tabelle ein, in der der Datenfeed im Modell gespeichert werden soll.  
  
     Standardmäßig wird der Name des Reporting Services-Steuerelements verwendet, wenn kein Name zugewiesen wurde: z. B. Tablix1, Tablix2. Es wird empfohlen, diesen Namen beim Import zu ändern, damit Sie den Ursprung des importierten Datenfeeds einfacher identifizieren können.  
  
11. Klicken Sie auf **Vorschau anzeigen und filtern** , um die Daten zu überprüfen und die Spaltenauswahl zu ändern. Sie können die Zeilen, die in den Berichtsdatenfeed importiert werden, nicht einschränken. Sie können jedoch Spalten entfernen, indem Sie die entsprechenden Kontrollkästchen deaktivieren. Klicken Sie auf **OK**.  
  
12. Klicken Sie auf der Seite **Tabellen und Sichten auswählen** auf **Fertig stellen**.  
  
## <a name="see-also"></a>Siehe auch  
 [Unterstützte Datenquellen &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)   
 [Unterstützte Datentypen &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md)   
 [Identitätswechsel &#40; SSAS – tabellarisch &#41;](../../analysis-services/tabular-models/impersonation-ssas-tabular.md)   
 [Verarbeiten von Daten &#40;SSAS – tabellarisch&#41;](../../analysis-services/tabular-models/process-data-ssas-tabular.md)   
 [Importieren von Daten &#40;SSAS – tabellarisch&#41;](http://msdn.microsoft.com/library/6617b2a2-9f69-433e-89e0-4c5dc92982cf)  
  
  

