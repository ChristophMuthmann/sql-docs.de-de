---
title: "Vertrauenswürdiger Speicherort lässt keine externen datenverbindungen zu | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: dc0cedfd-a7d0-40ef-bdd6-ea508130640a
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f774f6bc9a4d950d8f7c00e3c3e79aa3211e4cf
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="trusted-location-does-not-allow-external-data-connections"></a>Vertrauenswürdiger Speicherort lässt keine externen datenverbindungen
  Für Excel-Arbeitsmappen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten enthalten, gibt Excel Services diesen Fehler zurück, wenn keine Verbindung mit eingebetteten Datenquellen hergestellt werden kann.  
  
## <a name="details"></a>Details  
  
|||  
|-|-|  
|Gilt für|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] für SharePoint|  
|Produktversion|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Ursache|Excel Services sind dafür konfiguriert, den externen Datenzugriff zu verweigern.|  
|Meldungstext|Der vertrauenswürdige Speicherort, an dem die Arbeitsmappe gespeichert wird, lässt keine externen Datenverbindungen zu. Die folgenden Verbindungen wurden nicht aktualisiert: [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten|  
  
## <a name="explanation"></a>Erklärung  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten eingebettete Datenverbindungen. Um die Interaktion mit Arbeitsmappen über Slicer und Filter zu unterstützen, müssen Excel Services so konfiguriert sein, dass der externe Datenzugriff über eingebettete Verbindungsinformationen möglich ist. Externer Datenzugriff ist zum Abrufen von [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Daten erforderlich, die auf [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Server in der Farm geladen wurden.  
  
## <a name="user-action"></a>Benutzeraktion  
 Ändern Sie die Konfigurationseinstellungen, um eingebettete Datenquellen zuzulassen.  
  
1.  Klicken Sie in der Zentraladministration unter Anwendungsverwaltung auf **Dienstanwendungen verwalten**.  
  
2.  Klicken Sie auf **Excel Services-Anwendung**.  
  
3.  Klicken Sie auf **Vertrauenswürdiger Dateispeicherort**.  
  
4.  Klicken Sie auf **http://** oder den Speicherort, den Sie konfigurieren möchten.  
  
5.  Klicken Sie unter Externe Daten in **Externe Daten zulassen**auf Vertrauenswürdige Datenverbindungsbibliotheken und eingebettete Verbindungen.  
  
6.  Klicken Sie auf **OK**.  
  
 Alternativ können Sie einen neuen vertrauenswürdigen Speicherort für Websites erstellen, die [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] -Arbeitsmappen enthalten, und dann die Konfigurationseinstellungen nur für diese Website ändern. Weitere Informationen finden Sie unter [Erstellen eines vertrauenswürdigen Speicherorts für PowerPivot-Websites in der Zentraladministration](../../analysis-services/power-pivot-sharepoint/create-a-trusted-location-for-power-pivot-sites-in-central-administration.md).  
  
  

