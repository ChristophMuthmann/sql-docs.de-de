---
title: SQL Server 2012 SP1 Release Notes | Microsoft-Dokumentation
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-non-specified
ms.technology: server-general
ms.custom: 
ms.date: 01/31/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72171357-28de-4edd-bdfd-194f97225a6f
caps.latest.revision: 
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac1dcd75aa97cb12142d142c82d5c0c6d3f59791
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/27/2018
---
# <a name="sql-server-2012-sp1-release-notes"></a>SQL Server 2012 SP1 Release Notes
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]
In diesen Versionsanmerkungen werden bekannte Probleme beschrieben, mit denen Sie sich vertraut machen sollten, bevor Sie mit der Installation oder Problembehandlung in [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1 beginnen. Die Anmerkungen zu dieser Version sind nur online und nicht auf den Installationsmedien verfügbar und werden regelmäßig aktualisiert.  
  
## <a name="bkmk_top"></a>Inhalt  
[1.0 Vor der Installation](#bmk_Install)  
  
[2.0 Analysis Services und PowerPivot](#bkmk_AS)  
  
[3.0 Reporting Services](#bkmk_RS)  
  
[4.0 Data Quality Services](#bkmk_DQS)  
  
[5.0 SQL Server Express](#bkmk_Express)  
  
[6.0 Change Data Capture Service und Designer für Oracle von Attunity](#bkmk_CDC)  
  
[7.0 SQL Server Data-Tier Application Framework (DACFx)](#DACFx)  
  
[8.0 Bekannte Probleme, die in diesem Service Pack behoben wurden](#bkmk_known_issues_fixed)  
  
## <a name="bmk_Install"></a>1.0 Vor der Installation  
Vor der Installation von SQL Server 2012 SP1 sollten folgende Informationen beachtet werden.  
  
### <a name="11-reinstalling-an-instance-of-sql-server-failover-custer-fails-if-you-use-the-same-ip-address"></a>1.1 Die Neuinstallation einer SQL Server-Failoverclusterinstanz verursacht einen Fehler, wenn dieselbe IP-Adresse verwendet wird  
**Problem:** Wenn Sie während der Installation einer SQL Server-Failoverclusterinstanz eine falsche IP-Adresse angeben, tritt ein Fehler auf. Wenn Sie nach der Deinstallation der fehlerhaften Instanz versuchen, die SQL Server-Failoverclusterinstanz mit demselben Instanznamen und der richtigen IP-Adresse erneut zu installieren, schlägt die Installation fehl. Dies liegt daran, dass noch die doppelte Ressourcengruppe aus der vorherigen Installation vorhanden ist.  
  
**Problemumgehung:** Um dieses Problem zu beheben, verwenden Sie während der Neuinstallation einen anderen Instanznamen oder löschen die Ressourcengruppe vor der Neuinstallation manuell. Weitere Informationen finden Sie unter [Hinzufügen oder Entfernen von Knoten in einem SQL Server-Failovercluster](http://msdn.microsoft.com/library/ms191545).  
  
### <a name="12-choose-the-correct-file-to-download-and-install"></a>1.2 Auswählen der richtigen Download- und Installationsdatei  
Bestimmen Sie mithilfe der folgenden Tabelle, welche Datei heruntergeladen und installiert werden muss. Stellen Sie sicher, dass die Systemanforderungen erfüllt sind, bevor Sie das Service Pack installieren. Die Systemanforderungen sind auf den Downloadseiten angegeben, die mit den Links in der Tabelle verknüpft sind.  
  
|Aktuell installierte Version...|Gewünschter Vorgang...|Download und Installation von...|  
|-------------------------------------------|----------------------|---------------------------|  
|**32-Bit-Installationen:**|||  
|32-Bit-Version einer beliebigen Edition von SQL Server 2012|Upgrade auf die 32-Bit-Version von SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Eine 32-Bit-Version von SQL Server 2012 RTM Express|Upgrade auf die 32-Bit-Version von SQL Server 2012 Express SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32-Bit-Version nur der Client- und Verwaltbarkeitstools für SQL Server 2012 (einschließlich SQL Server 2012 Management Studio)|Upgrade der Client- und Verwaltbarkeitstools auf die 32-Bit-Version von SQL Server 2012 SP1|SQLManagementStudio_x86_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Eine 32-Bit-Version von SQL Server 2012 Management Studio Express|Upgrade auf die 32-Bit-Version von SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x86_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|32-Bit-Version einer beliebigen Edition von SQL Server 2012 **und** 32-Bit-Version der Client- und Verwaltbarkeitstools (einschließlich SQL Server 2012 RTM Management Studio)|Upgrade aller Produkte auf die 32-Bit-Version von SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x86-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|32-Bit-Version von mindestens einem Tool aus dem [Feature Pack für Microsoft SQL Server 2012 RTM](http://www.microsoft.com/download/details.aspx?id=16978)|Upgrade der Tools auf die 32-Bit-Version des Feature Packs für Microsoft SQL Server 2012 SP1|Mindestens eine Datei aus dem [Feature Pack für Microsoft SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Keine 32-Bit-Installation von SQL Server 2012|Installation von Server 2012 in der 32-Bit-Version einschließlich SP1 (neue Instanz mit vorinstalliertem SP1)|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **und** SQLServer2012SP1-FullSlipstream-x86-ENU.box über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Keine 32-Bit-Installation von SQL Server 2012 Management Studio|Installation von SQL Server 2012 Management Studio in der 32-Bit-Version einschließlich SP1|SQLManagementStudio_x86_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Keine 32-Bit-Version von SQL Server 2012 RTM Express|Installation von SQL Server 2012 Express in der 32-Bit-Version einschließlich SP1|SQLEXPR32_x86_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkId=267905)|  
|Eine 32-Bit-Installation von **SQL Server 2008** oder **SQL Server 2008 R2**|**Direktes Upgrade** auf die 32-Bit-Version von SQL Server 2012 einschließlich SP1|SQLServer2012SP1-FullSlipstream-x86-ENU.exe **und** SQLServer2012SP1-FullSlipstream-x86-ENU.box über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|**64-Bit-Installationen:**|||  
|64-Bit-Version einer beliebigen Edition von SQL Server 2012|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64-Bit-Version von SQL Server 2012 RTM Express|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64-Bit-Version ausschließlich der Client- und Verwaltbarkeitstools für SQL Server 2012 (einschließlich SQL Server 2012 Management Studio)|Upgrade der Client- und Verwaltbarkeitstools auf die 64-Bit-Version von SQL Server 2012 SP1|SQLManagementStudio_x64_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64-Bit-Version von SQL Server 2012 Management Studio Express|Upgrade auf die 64-Bit-Version von SQL Server 2012 SP1 Management Studio Express|SQLManagementStudio_x64_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|64-Bit-Version einer beliebigen Edition von SQL Server 2012 **und** 64-Bit-Version der Client- und Verwaltbarkeitstools (einschließlich SQL Server 2012 RTM Management Studio)|Upgrade aller Produkte auf die 64-Bit-Version von SQL Server 2012 SP1|SQLServer2012SP1-KB2674319-x64-ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|64-Bit-Version von mindestens einem Tool aus dem [Feature Pack für Microsoft SQL Server 2012 RTM](http://www.microsoft.com/download/en/details.aspx?id=16978)|Upgrade der Tools auf die 64-Bit-Version des Feature Packs für Microsoft SQL Server 2012 SP1|Mindestens eine Datei aus dem [Feature Pack für Microsoft SQL Server 2012 SP1](http://go.microsoft.com/fwlink/p/?LinkID=268266)|  
|Keine 64-Bit-Installation von SQL Server 2012|Installation von Server 2012 in der 64-Bit-Version einschließlich SP1 (neue Instanz mit vorinstalliertem SP1)|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **und** SQLServer2012SP1-FullSlipstream-x64-ENU.box über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
|Keine 64-Bit-Installation von SQL Server 2012 Management Studio|Installation von SQL Server 2012 Management Studio in der 64-Bit-Version einschließlich SP1|SQLManagementStudio_x64_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Keine 64-Bit-Version von SQL Server 2012 RTM Express|Installation von SQL Server 2012 Express in der 64-Bit-Version einschließlich SP1|SQLEXPR_x64_ENU.exe über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=267905)|  
|Eine 64-Bit-Installation von **SQL Server 2008** oder **SQL Server 2008 R2**|**Direktes Upgrade** auf die 64-Bit-Version von SQL Server 2012 einschließlich SP1|SQLServer2012SP1-FullSlipstream-x64-ENU.exe **und** SQLServer2012SP1-FullSlipstream-x64-ENU.box über [diesen Link](http://go.microsoft.com/fwlink/p/?LinkID=268158)|  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../sql-server/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Inhalte](#bkmk_top)  
  
## <a name="bkmk_AS"></a>2.0 Analysis Services und PowerPivot  
  
### <a name="21-powerpivot-configuration-tool-does-not-create-the-powerpivot-gallery"></a>2.1 Der PowerPivot-Katalog wird vom PowerPivot-Konfigurationstool nicht erstellt  
**Problem:** Das PowerPivot-Konfigurationstool stellt eine Teamwebsite bereit, und daher wird der PowerPivot-Katalog nicht erstellt.  
  
**Problemumgehung:** Erstellen Sie eine neue App (Bibliothek).  
  
1.  Überprüfen Sie, ob die Websitesammlungsfunktion **Funktion zur PowerPivot-Integration für Websitesammlungen** aktiv ist.  
  
2.  Klicken Sie auf der Seite **Websiteinhalt** einer vorhandenen Website auf **App hinzufügen**.  
  
3.  Klicken Sie auf **PowerPivot-Katalog**.  
  
### <a name="22-to-use-powerpivot-for-excel-with-excel-2013-you-must-use-the-add-in-that-is-installed-with-excel"></a>2.2 Zur Verwendung von PowerPivot für Excel mit Excel 2013 müssen Sie das mit Excel installierte Add-In verwenden  
**Problem:** Bei Office 2010 ist PowerPivot für Excel ein eigenständiges Add-In, das von [http://www.microsoft.com/bi/powerpivot.aspx](http://www.microsoft.com/bi/powerpivot.aspx)heruntergeladen werden kann. Alternativ kann es auch vom [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=29074)heruntergeladen werden. Beachten Sie, dass zwei Versionen des PowerPivot-Add-Ins als Download verfügbar sind: Eine Version im Lieferumfang von SQL Server 2008 R2 und eine weitere im Lieferumfang von SQL Server 2012. Im Falle von Office 2013 ist PowerPivot für Excel jedoch im Lieferumfang von Office enthalten und wird zusammen mit Excel installiert. Während die SQL Server 2008 R2- und SQL Server 2012-Versionen von PowerPivot für Excel 2010 nicht mit Excel 2013 kompatibel sind, können Sie weiterhin PowerPivot für Excel 2010 auf dem Clientcomputer installieren, wenn Sie Excel 2010 parallel zu Excel 2013 ausführen möchten. Da die beiden Excel-Versionen gleichzeitig vorhanden sein können, gilt dies auch für die entsprechenden PowerPivot-Add-Ins.  
  
**Problemumgehung:** Um PowerPivot für Excel 2013 zu verwenden, müssen Sie das COM-Add-In aktivieren. Wählen Sie in Excel 2013 **Datei** | **Optionen** | **Add-Ins**aus. Wählen Sie im Dropdownfeld **Verwalten** die Option **COM-Add-Ins** aus, und klicken Sie auf **Ausführen**. Wählen Sie unter **COM-Add-Ins**die Option **Microsoft Office PowerPivot für Excel 2013** aus, und klicken Sie auf **OK**.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../sql-server/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Inhalte](#bkmk_top)  
  
## <a name="bkmk_RS"></a>3.0 Reporting Services  
  
### <a name="31-install-and-configure-sharepoint-server-2013-prior-to-installing-reporting-services"></a>3.1 SharePoint Server 2013 muss vor der Installation von Reporting Services installiert und konfiguriert werden  
**Problem:** Führen Sie die folgenden erforderlichen Schritte aus, **bevor** Sie SQL Server Reporting Services (SSRS) installieren.  
  
1.  Führen Sie das Vorbereitungstool für SharePoint 2013-Produkte aus.  
  
2.  Installieren Sie SharePoint Server 2013.  
  
3.  Führen Sie den Konfigurations-Assistenten für SharePoint 2013-Produkte oder die entsprechenden Konfigurationsschritte aus, um die SharePoint-Farm zu konfigurieren.  
  
**Problemumgehung:**  Wenn Sie den SharePoint-Modus von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] vor der Konfiguration der SharePoint-Farm installiert haben, richtet sich die erforderliche Problemumgehung danach, welche weiteren Komponenten installiert sind.  
  
### <a name="32-power-view-in-sharepoint-server-2013-requires-microsoftanalysisservicesspclientdll"></a>3.2 Power View erfordert in SharePoint Server 2013 "Microsoft.AnalysisServices.SPClient.dll"  
**Problem:** Die erforderliche Komponente **Microsoft.AnalysisServices.SPClient.dll** wird von [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] nicht installiert. Wenn Sie die Vorschauversion von SharePoint Server 2013 und [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] im SharePoint-Modus installieren, ohne das Installationspaket für PowerPivot für SharePoint 2013 **spPowerPivot.msi** herunterzuladen und zu installieren, ist Power View nicht funktionsfähig und zeigt folgende Symptome.  
  
**Symptome:** Beim Erstellen eines Power View-Berichts wird eine mit der folgenden vergleichbare Fehlermeldung ausgegeben:  
  
-   "Es kann keine Verbindung mit der Datenquelle hergestellt werden..."  
  
Die internen Fehlerdetails enthalten eine mit der folgenden vergleichbare Meldung:  
  
-   "Der Wert 'SharePoint Principal' wird für die User Identity-Eigenschaft der Verbindungszeichenfolge nicht unterstützt."  
  
**Problemumgehung:** Installieren Sie das Installationspaket für PowerPivot für SharePoint 2013 (**spPowerPivot.msi**) unter SharePoint Server 2013. Das Installationspaket ist als Teil des [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Packs verfügbar. Das Feature Pack kann vom [!INCLUDE[msCoName](../includes/msconame-md.md)] Download Center unter [SQL Server 2012 SP1 Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)heruntergeladen werden.  
  
### <a name="33-power-view-sheets-in-a-powerpivot-workbook-are-deleted-after-a-scheduled-data-refresh"></a>3.3 Power View-Blätter in einer PowerPivot-Arbeitsmappe werden nach einer geplanten Datenaktualisierung gelöscht  
**Problem:**Wenn Sie im PowerPivot-Add-In für SharePoint **Scheduled Data Refresh** für eine Power View-Arbeitsmappe verwenden, werden alle Power View-Blätter gelöscht.  
  
**Problemumgehung**: Um **Scheduled Data Refresh** mit Power View-Arbeitsmappen zu verwenden, erstellen Sie eine PowerPivot-Arbeitsmappe, die nur das Datenmodell enthält. Erstellen Sie eine separate Arbeitsmappe mit Excel-Tabellen und Power View-Blättern, die mit der PowerPivot-Arbeitsmappe verknüpft ist, in der das Datenmodell enthalten ist. Nur die PowerPivot-Arbeitsmappe mit dem Datenmodell sollte für die geplante Datenaktualisierung verwendet werden.  
  
## <a name="bkmk_DQS"></a>4.0 Data Quality Services  
  
### <a name="41-dqs-available-in-the-incorrect-edition-of-sql-server-2012"></a>4.1 DQS ist in der falschen Edition von SQL Server 2012 verfügbar  
**Problem:** In der RTM-Version von [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] ist die Data Quality Services (DQS)-Funktion in anderen SQL Server-Editionen als Enterprise, Business Intelligence und Developer verfügbar. Nach der Installation von SQL Server 2012 SP1 ist DQS in allen Editionen außer Enterprise, Business Intelligence und Developer nicht verfügbar.  
  
**Problemumgehung**: Wenn Sie DQS in einer nicht unterstützten Edition verwenden, führen Sie entweder ein Upgrade auf eine unterstützte Edition aus oder entfernen die Abhängigkeit von dieser Funktion aus den Anwendungen.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../sql-server/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Inhalte](#bkmk_top)  
  
## <a name="bkmk_Express"></a>5.0 SQL Server Express  
  
### <a name="51-full-version-of-sql-server-management-studio-available-in-sql-server-2012-express-sp1"></a>5.1 In SQL Server 2012 Express SP1 ist die Vollversion von SQL Server Management Studio verfügbar  
Die SQL Server 2012 Express Service Pack 1 (SP1)-Version umfasst anstelle von SQL Server 2012 Management Studio Express die Vollversion von SQL Server 2012 Management Studio (die zuvor nur auf der SQL Server 2012-DVD verfügbar war). Unter [SQL Server 2012 Express Service Pack 1](http://go.microsoft.com/fwlink/p/?linkid=267905)können Sie SQL Server 2012 Express SP1 herunterladen und installieren.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../sql-server/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Inhalte](#bkmk_top)  
  
## <a name="bkmk_CDC"></a>6.0 Change Data Capture Service und Designer für Oracle von Attunity  
  
### <a name="61-upgrading-the-cdc-service-and-designer"></a>6.1 Aktualisieren von CDC Service und Designer  
**Problem:** Wenn zu dem Zeitpunkt, zu dem Sie SQL Server 2012 SP1 installieren, der Change Data Capture Designer für Oracle und Change Data Capture Service für Oracle von Attunity auf dem Computer installiert sind, werden diese Komponenten durch die Installation von SP1 nicht aktualisiert.  
  
**Problemumgehung:** So aktualisieren Sie die CDC-Komponenten auf die neueste Version:  
  
1.  Laden Sie die MSI-Dateien für den Change Data Capture Service für Oracle von Attunity von der [Downloadseite für das SQL Server 2012 SP1-Feature Pack](http://go.microsoft.com/fwlink/p/?LinkID=268266)herunter.  
  
2.  Führen Sie die MSI-Datei aus.  
  
![Pfeilsymbol mit dem Link „Zurück zum Anfang“](../sql-server/media/uparrow16x16.gif "Pfeilsymbol mit dem Link „Zurück zum Anfang“")[Inhalte](#bkmk_top)  
  
## <a name="DACFx"></a>7.0 SQL Server Data-Tier Application Framework (DACFx)  
**Unterstützung für direkte Upgrades**  
  
Diese DACFx-Version (Data-Tier Application Framework) unterstützt direkte Upgrades von Vorgängerversionen. Somit müssen vorherige DACFx-Installationen vor dem Upgrade auf diese Version nicht entfernt werden. Zukünftige Versionen von DACFx finden Sie [hier](https://msdn.microsoft.com/library/dn702988.aspx).  
  
**Unterstützung für den selektiven XML-Index**  
  
SQL Server 2012 SP1 bietet Unterstützung für den [selektiven XML-Index (SXI)](http://msdn.microsoft.com/en-us/598ecdcd-084b-4032-81b2-eed6ae9f5d44), eine neue SQL Server-Funktion, die eine neuen leistungsfähigeren und effizienteren Ansatz zur Indizierung von XML-Spaltendaten darstellt.  
  
DACFx unterstützt jetzt SXI-Indizes in allen DAC-Szenarien und -Clienttools. SXI wird erst ab der neuesten SSDT-Version unterstützt. Die RTM-Version von SSDT und die SSDT-Version von September 2012 unterstützen kein SXI.  
  
**Unterstützung für das native BCP-Datenformat**  
  
Früher wurde das JSON-Datenformat verwendet, um Tabellendaten in DACPAC- und BACPAC-Paketen zu speichern. Ab diesem Update gewährleistet das systemeigene BCP-Format die Persistenz von Daten. Diese Neuerung bringt DACFx eine höhere Genauigkeit bei der Übernahme von SQL Server-Datentypen. Darüber hinaus schließt sie Unterstützung für SQL_Variant-Typen sowie eine verbesserte Datenbereitstellungsleistung bei umfangreichen Datenbanken ein.  
  
**Beibehaltung des Zustands von CHECK-Einschränkungen bei der Erstellung/Bereitstellung von Paketen**  
  
Früher wurde der Zustand von CHECK-Einschränkungen (WITH CHECK/NOCHECK), der für Tabellen im Datenbankschema definiert wurde, nicht beibehalten bzw. nicht in DACPAC-Dateien gespeichert. Dieses Verhalten kann zu Problemen bei der Paketbereitstellung führen, wenn CHECK-Einschränkungen durch bestehende Tabellendaten verletzt werden. Ab diesem Update speichert DACFx den aktuellen Zustand von CHECK-Einschränkungen in der DACPAC-Datei, wenn diese aus einer Datenbank extrahiert wird, und stellt den Zustand bei der Paketbereitstellung ordnungsgemäß wieder her.  
  
**Updates auf „SqlPackage.exe“ (DACFx-Befehlszeilentool)**  
  
-   Extrahieren einer DACPAC-Datei mit Daten: Erstellt eine Datenbank-Momentaufnahmedatei (.dacpac) von einer SQL Server- oder Windows Azure SQL-Livedatenbank, die zusätzlich zum Datenbankschema Daten aus Benutzertabellen enthält. Diese Pakete können mithilfe der Veröffentlichungsaktion von SqlPackage.exe auf einer neuen oder bestehenden SQL Server- oder Windows Azure SQL-Datenbank veröffentlicht werden. Die im Paket enthaltenen Daten ersetzen die bestehenden Daten in der Zieldatenbank.  
  
-   Exportieren einer BACPAC-Datei: Erstellt eine logische Sicherungsdatei (.bacpac) einer SQL Server- oder Windows Azure SQL-Livedatenbank, die das Datenbankschema und die Benutzerdaten enthält. Diese können verwendet werden, um eine Datenbank von einer lokalen SQL Server-Datenbank zu einer Windows Azure SQL-Datenbank zu migrieren. Mit Azure kompatible Datenbanken können exportiert und später zwischen unterstützten Versionen von SQL Server importiert werden.  
  
-   Importieren einer BACPAC-Datei: Importiert eine BACPAC-Datei, um eine neue SQL Server- oder Windows Azure SQL-Datenbank zu erstellen bzw. eine leere Datenbank mit Daten aufzufüllen.  
  
Eine vollständige Dokumentation zu SqlPackage.exe auf MSDN finden Sie [hier](http://msdn.microsoft.com/library/hh550080%28v=vs.103%29.aspx).  
  
**Paketkompatibilität**  
  
Mit dieser Version werden mehrere Szenarien für die Aufwärtskompatibilität von DAC-Paketen eingeführt.  
  
-   Mit dieser Version erstellte DAC-Pakete, die keine SXI-Elemente oder -Tabellendaten enthalten, können von DACFx-Vorgängerversionen (SQL Server 2012 RTM, SQL Server 2012 CU1 und DACFx von September 2012) verwendet werden.  
  
-   Alle von DACFx-Vorgängerversionen erstellten DAC-Pakete können von dieser Version verwendet werden.  
  
## <a name="bkmk_known_issues_fixed"></a>8.0 Bekannte Probleme, die in diesem Service Pack behoben wurden  
Eine vollständige Liste von Fehlern und bekannten Problemen, die in diesem Service Pack behoben wurden, finden Sie in diesem [KB-Artikel](http://support.microsoft.com/kb/2674319).  
  
[Inhalt](#bkmk_top)  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[Ermitteln der Version und Edition von SQL Server](http://support.microsoft.com/kb/321185)  
[Von den SQL Server 2014-Editionen unterstützte Funktionen](http://msdn.microsoft.com/en-us/5da61ff5-12b9-48e6-b3c8-0dacca1751c4)  
  
