---
title: "Diese Arbeitsmappe enthält eine oder mehrere Abfragen, die Aktualisierung der externen Daten | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: aa65c992-eb41-4032-9e11-a9ba871b6a3c
caps.latest.revision: 8
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f400a5513fcd16ea5344157e451d06b8fe103796
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="this-workbook-contains-one-or-more-queries-that-refresh-external-data"></a>Diese Arbeitsmappe enthält eine oder mehrere Abfragen, die Aktualisierung der externen Daten
  Für Excel-Arbeitsmappen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten, zeigt Excel Services diese Warnung an, wenn Verbindungsinformationen erkannt werden, und fordert Sie auf, Abfragen für diese Arbeitsmappe zu aktivieren oder deaktivieren.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Produktname|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro_md](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11_md](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)]|  
|Ursache|Excel Services ist so konfiguriert, dass bei Datenaktualisierungen Warnungen ausgegeben werden.|  
|Meldungstext|Diese Arbeitsmappe enthält eine oder mehrere Abfragen, die externe Daten aktualisieren. Ein böswilliger Benutzer kann eine Abfrage entwerfen, um auf vertrauliche Informationen zuzugreifen und sie an andere Benutzer zu verteilen oder andere schädliche Aktionen auszuführen.<br /><br /> Wenn Sie der Quelle dieser Arbeitsmappe vertrauen, klicken Sie auf Ja, um Abfragen für externe Daten in dieser Arbeitsmappe zu aktivieren. Wenn Sie sich nicht sicher sind, klicken Sie auf Nein, damit Änderungen nicht für die Arbeitsmappe übernommen werden.<br /><br /> Möchten Sie Abfragen für externe Daten in dieser Arbeitsmappe aktivieren?|  
  
## <a name="explanation"></a>Erklärung  
 [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten eingebettete Datenverbindungszeichenfolgen, die von Excel verwendet werden, um mit einem externen [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Server zu kommunizieren, der die Daten lädt und berechnet. Wenn Warnungen bei Datenaktualisierungen aktiviert sind, erkennt Excel Services diese Verbindungszeichenfolge und warnt den Benutzer entsprechend.  
  
 Abfragen müssen aktiviert sein, um [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Daten in der Arbeitsmappe zu filtern und sie in Slices aufzuteilen. Stellen Sie sicher, dass Sie Abfragen nur für diejenigen [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappen aktivieren, denen Sie vertrauen.  
  
## <a name="user-action"></a>Benutzeraktion  
 Klicken Sie auf **Ja** , um Abfragen zu aktivieren.  
  
 Sie können auch die Konfigurationseinstellungen ändern, damit keine Warnungen bei Aktualisierungen mehr angezeigt werden:  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf **Excel Services-Anwendung**.  
  
3.  Klicken Sie auf **Vertrauenswürdiger Dateispeicherort**.  
  
4.  Klicken Sie auf **http://** oder den Speicherort, den Sie konfigurieren möchten.  
  
5.  Deaktivieren Sie in „Externe Daten“ das Kontrollkästchen **Beim Aktualisieren warnen**.  
  
6.  Klicken Sie auf **OK**.  
  
 Alternativ können Sie einen neuen vertrauenswürdigen Speicherort für Websites erstellen, die [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten, und dann die Konfigurationseinstellungen nur für diese Website ändern. Weitere Informationen finden Sie unter [Erstellen eines vertrauenswürdigen Speicherorts für PowerPivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  

