---
title: "Diese Arbeitsmappe enth&#228;lt eine oder mehrere Abfragen, die externe Daten aktualisieren. | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
caps.latest.revision: 8
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 7
---
# Diese Arbeitsmappe enth&#228;lt eine oder mehrere Abfragen, die externe Daten aktualisieren.
  Für Excel-Arbeitsmappen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Daten enthalten, zeigt Excel Services diese Warnung an, wenn Verbindungsinformationen erkannt werden, und fordert Sie auf, Abfragen für diese Arbeitsmappe zu aktivieren oder deaktivieren.  
  
## Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Excel Services ist so konfiguriert, dass bei Datenaktualisierungen Warnungen ausgegeben werden.|  
|Meldungstext|Diese Arbeitsmappe enthält eine oder mehrere Abfragen, die externe Daten aktualisieren. Ein böswilliger Benutzer kann eine Abfrage entwerfen, um auf vertrauliche Informationen zuzugreifen und sie an andere Benutzer zu verteilen oder andere schädliche Aktionen auszuführen.<br /><br /> Wenn Sie der Quelle dieser Arbeitsmappe vertrauen, klicken Sie auf Ja, um Abfragen für externe Daten in dieser Arbeitsmappe zu aktivieren. Wenn Sie sich nicht sicher sind, klicken Sie auf Nein, damit Änderungen nicht für die Arbeitsmappe übernommen werden.<br /><br /> Möchten Sie Abfragen für externe Daten in dieser Arbeitsmappe aktivieren?|  
  
## Erklärung  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten eingebettete Datenverbindungszeichenfolgen, die von Excel verwendet werden, um mit einem externen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Server zu kommunizieren, der die Daten lädt und berechnet. Wenn Warnungen bei Datenaktualisierungen aktiviert sind, erkennt Excel Services diese Verbindungszeichenfolge und warnt den Benutzer entsprechend.  
  
 Abfragen müssen aktiviert sein, um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Daten in der Arbeitsmappe zu filtern und sie in Slices aufzuteilen. Stellen Sie sicher, dass Sie Abfragen nur für diejenigen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]-Arbeitsmappen aktivieren, denen Sie vertrauen.  
  
## Benutzeraktion  
 Klicken Sie auf **Ja**, um Abfragen zu aktivieren.  
  
 Sie können auch die Konfigurationseinstellungen ändern, damit keine Warnungen bei Aktualisierungen mehr angezeigt werden:  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf **Excel Services-Anwendung**.  
  
3.  Klicken Sie auf **Vertrauenswürdiger Dateispeicherort**.  
  
4.  Klicken Sie auf **http://** oder den Speicherort, den Sie konfigurieren möchten.  
  
5.  Deaktivieren Sie in „Externe Daten“ das Kontrollkästchen **Beim Aktualisieren warnen**.  
  
6.  Klicken Sie auf **OK**.  
  
 Alternativ können Sie einen neuen vertrauenswürdigen Speicherort für Websites erstellen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten, und dann die Konfigurationseinstellungen nur für diese Website ändern. Weitere Informationen finden Sie unter [Erstellen eines vertrauenswürdigen Speicherorts für PowerPivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  