---
title: Verwenden einer Office Data Connection (.odc) mit Berichten | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-data
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Office Data Connection (.odc) files
- SharePoint integration [Reporting Services], shared data sources
- .odc files
ms.assetid: e8d6896d-f886-4390-8b5d-96f0a50c250c
caps.latest.revision: "13"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 68cbb3437a7f994a60e13163a8372f2e5c0a7174
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="use-an-office-data-connection-odc-with-reports"></a>Verwenden einer Office Data Connection (.odc) mit Berichten
  Bei beschränkten Szenarien können Sie eine vorhandene Office Data Connection (.odc)-Datei verwenden, um Verbindungsinformationen für einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht bereitzustellen. Sie können beim Erstellen einer freigegebenen Datenquelle eine ODC-Datei statt einer RSDS-Datei verwenden. Eine ODC-Datei wird vom Berichtsserver auf dieselbe Weise verwendet wie eine RSDS-Datei. Die Datei wird gelesen, um den Datenquellentyp, eine Verbindungszeichenfolge und Anmeldeinformationen abzurufen.  
  
 Nicht alle ODC-Dateien können für einen [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] -Bericht verwendet werden. Anhand der Datenverarbeitungserweiterung und der Merkmale des Berichts und der ODC-Datei wird bestimmt, ob eine ODC-Datei verwendet werden kann:  
  
-   Der Bericht muss für die Verwendung mit einem OLE DB- oder ODBC-Datenanbieter entworfen sein. Wenn Sie den Bericht mithilfe einer anderen Datenverarbeitungserweiterung erstellt haben, enthält der Bericht oder enthalten dessen Dateien möglicherweise Funktionen, die nicht vom OLE DB- oder ODBC-Datenanbieter unterstützt werden.  
  
-   Die ODC-Datei muss über die erwarteten Elemente und die erwartete Struktur verfügen. Der Datenanbieter und die Einstellungen für die Anmeldeinformationen müssen explizit in der Datei festgelegt sein, damit sie vom Berichtsserver gelesen werden können. Die einfachste Methode, diese Werte festzulegen, besteht darin, die ODC-Datei vor dem Hochladen in die SharePoint-Bibliothek zu exportieren.  
  
-   Die ODC-Datei muss den Verbindungstyp OLE DB oder ODBC angeben.  
  
-   In der ODC-Datei muss eine Verbindungszeichenfolge angegeben sein.  
  
-   Die Anmeldeinformationen können auf **None**, **Stored**oder **Integrated**festgelegt werden. Wenn die Methode für die Anmeldeinformationen auf **Stored**festgelegt ist, wird der Benutzer vom Berichtsserver zur Eingabe seiner Anmeldeinformationen aufgefordert, und es werden nicht die gespeicherten Anmeldeinformationen verwendet. Vom Berichtsserver können wie in einer ODC-Datei definiert keine gespeicherten Anmeldeinformationen verwendet werden.  
  
-   Die Datenquelle muss über ein Schema verfügen, das mit dem zum Erstellen des Berichts verwendeten Schema identisch ist. Wenn die Datenstrukturen unterschiedlich sind, wird der Bericht nicht ausgeführt.  
  
-   Die ODC-Datei muss in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office 2007 erstellt werden. (Ältere Versionen von ODC-Dateien sind nicht kompatibel mit Berichtsdefinitionsdateien.)  
  
 Sie können keine ODC-Dateien verwenden, in denen Verbindungen mit Datenquellen angegeben sind, die auf einem Berichtsserver nicht verarbeitet werden können. Dies gilt auch, wenn die Datenquellentypen der ODC-Datei unterstützen Datenquellentypen ähneln. Insbesondere, wenn Sie eine ODC-Datei in Microsoft Excel 2007 erstellt haben, die Daten aus Microsoft Access, dem Web oder einer Textdatei abruft, können Sie mit dieser ODC-Datei keine Daten für einen Bericht bereitstellen.  
  
 Berichte und Modelle des Berichts-Generators werden für ODC-Dateien nicht unterstützt. Sie können eine ODC-Datei nicht zum Generieren eines Modells verwenden, und Sie können das Modell nicht so konfigurieren, dass eine freigegebene Datenquelle mit einem Link zu einer ODC-Datei verwendet wird.  
  
 Wenn Sie nicht mit ODC-Dateien vertraut sind, können Sie die folgenden Anweisungen zum Erstellen und Exportieren einer ODC-Datei verwenden. Eine einfache Möglichkeit, eine ODC-Datei für eine OLE DB-Datenquelle zu erstellen, besteht im Verwenden von Excel 2007 und dem Datenverbindungs-Assistenten. Beachten Sie, dass vom Assistenten keine Datenquelle erstellt wird. Sie müssen über eine externe Datenquelle verfügen, die bereits definiert ist.  
  
 Eine vorhandene ODC-Datei sollte nur verwendet werden, wenn sie vollständig mit dem Bericht und den Abfragen kompatibel ist. Wenn Fehler auftreten, die beträchtliche Änderungen am Bericht oder an der ODC-Datei erfordern, sollten Sie eine neue RSDS-Datei für den Bericht erstellen. Weitere Informationen zum Erstellen einer freigegebenen Datenquelle, die eine RSDS-Datei verwendet, finden Sie unter [Erstellen und Verwalten von freigegebenen Datenquellen (Reporting Services im integrierten SharePoint-Modus)](http://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76).  
  
### <a name="to-create-and-export-an-odc-file"></a>So erstellen und exportieren Sie eine ODC-Datei  
  
1.  Starten Sie Excel 2007.  
  
2.  Klicken Sie auf der Registerkarte **Daten** in der Gruppe **Externe Daten** auf **Aus anderen Quellen**, und klicken Sie anschließend auf **Vom Datenverbindungs-Assistent**.  
  
3.  Wählen Sie **Weitere/erweiterte**aus, und klicken Sie anschließend auf **Weiter**.  
  
4.  Wählen Sie **Microsoft OLE DB Provider for SQL Server**aus, und klicken Sie anschließend auf **Weiter**.  
  
5.  Geben Sie den Namen des Servers (standardmäßig der Netzwerkname des Computers) und ein Benutzerkonto ein, das über eine gültige Anmeldung und Datenbankberechtigungen verfügt. Klicken Sie auf **Weiter**.  
  
6.  Wählen Sie eine Datenbank aus, und klicken Sie anschließend auf **OK** , um das Dialogfeld **Datenlinkeigenschaften** zu schließen.  
  
7.  Das Kontrollkästchen **Mit einer ausgewählten Tabelle verbinden:** ist standardmäßig aktiviert. Es wird zum Abrufen von Daten aus einer spezifischen Tabelle verwendet. Es werden alle Abfragen in einer ODC-Datei vom Berichtsserver ignoriert. Daher ist es nicht ausschlaggebend, ob Sie das Kontrollkästchen aktivieren oder deaktivieren. Abfragen, mit denen Daten für einen Bericht abgerufen werden, befinden sich in der Berichtsdefinitionsdatei, nicht in externen Dateien.  
  
8.  Während die Verbindung geöffnet ist, können Sie Eigenschaften bearbeiten und die Verbindungsdatei exportieren. Klicken Sie auf der Registerkarte **Daten** in der Gruppe **Verbindungen** auf **Eigenschaften**, und klicken Sie anschließend neben dem Namen der Verbindung auf die Schaltfläche **Verbindungseigenschaften** .  
  
9. Klicken Sie auf der Registerkarte **Definition** auf **Verbindungsdatei exportieren**.  
  
10. Geben Sie einen Namen für die Datei ein, und klicken Sie dann auf **Speichern**. Schließen Sie die Anwendung und alle geöffneten Dateien.  
  
### <a name="to-upload-and-use-an-odc-file"></a>So laden Sie eine ODC-Datei hoch und verwenden Sie  
  
1.  Öffnen Sie die Bibliothek, in die Sie die Verbindungsdatei hochladen möchten.  
  
2.  Klicken Sie im Menü **Upload** auf **Dokumentupload**.  
  
3.  Klicken Sie auf **Durchsuchen**.  
  
4.  Wählen Sie die von Ihnen erstellte ODC-Datei aus. Die ODC-Datei befindet sich standardmäßig im Ordner Meine Dateien unter Meine Datenquellen.  
  
5.  Klicken Sie auf **Öffnen** , um die Datei auszuwählen, und klicken Sie auf **OK** , um die Auswahl zu speichern. Die Eigenschaftenseite für das neue Element wird automatisch geöffnet.  
  
6.  Wählen Sie unter Inhaltstyp die Option **Berichtsdatenquelle**aus, und klicken Sie anschließend auf **OK**.  
  
7.  Zeigen Sie auf einen Bericht.  
  
8.  Klicken Sie auf den Pfeil nach unten, und wählen Sie **Datenquellen verwalten**aus.  
  
9. KIicken Sie auf den Namen der Datenquelle.  
  
10. Wenn für den Bericht benutzerdefinierte Datenquelleninformationen verwendet werden, klicken Sie auf **Freigegeben**.  
  
11. Klicken Sie unter **Datenquellenlink**auf die Schaltfläche zum Durchsuchen (**...**).  
  
12. Wählen Sie die von Ihnen soeben hochgeladene ODC-Datei aus.  
  
13. Klicken Sie auf **OK** , um die Datei auszuwählen, und klicken Sie anschließend auf **OK** , um die Änderungen zu speichern.  
  
     Wenn Sie versuchen, diese Schritte für die [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] -Beispieldatenbank und -Beispielberichte auszuführen, sollten Sie beachten, dass nur der Bericht Company Sales sofort mit einer ODC-Datei verwendet werden kann. Die anderen Beispielberichte enthalten Abfrageparameter und Funktionen, die den OLE DB-Anbieter nicht unterstützen. Sie können die Berichte jedoch für den OLE DB-Anbieter aufbereiten, wenn Sie sie zuerst im Berichts-Designer ändern.  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Erstellen, Ändern und Löschen von freigegebenen Datenquellen &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md)  
  
  
