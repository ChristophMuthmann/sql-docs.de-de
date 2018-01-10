---
title: "Übergeben von Berichtsparametern innerhalb einer URL | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: reporting-services
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- URL access [Reporting Services], passing parameters
- passing parameters [Reporting Services]
ms.assetid: f93a94cc-27b5-435a-aa85-69e6ec6459ad
caps.latest.revision: "36"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Active
ms.openlocfilehash: 9ed073313d11f6764bc845ff1f993994add14f60
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/09/2018
---
# <a name="pass-a-report-parameter-within-a-url"></a>Übergeben von Berichtsparametern innerhalb einer URL
  Sie können Berichtsparameter an einen Bericht übergeben, indem Sie sie in eine Berichts-URL einschließen. Diesen URL-Parametern wird nichts vorangestellt, da sie direkt an das Berichtsverarbeitungsmodul übergeben werden.  
  
> [!IMPORTANT]  
>  Es ist wichtig, dass die URL die `_vti_bin` -Proxysyntax zur Weiterleitung der Anforderung über SharePoint sowie den [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] -HTTP-Proxy enthält. Durch den Proxy wird der HTTP-Anforderung Kontext hinzugefügt. Dieser ist erforderlich, damit der Bericht auf Berichtsservern im SharePoint-Modus ordnungsgemäß ausgeführt wird.  
>   
>  Wenn Sie keine Proxysyntax einschließen, müssen Sie dem Parameter *rp:*voranstellen.  
  
 Alle Abfrageparameter können über entsprechende Berichtsparameter verfügen. Sie übergeben einen Abfrageparameter an einen Bericht, indem Sie den entsprechenden Berichtsparameter übergeben. Weitere Informationen finden Sie unter [Erstellen einer Abfrage im Relationalen Abfrage-Designer (Berichts-Generator und SSRS)](../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]  
>  Bei den Berichtsparametern wird die Groß-/Kleinschreibung beachtet.  
  
> [!NOTE]  
>  Bei Berichtsparametern wird zwischen Groß-/Kleinschreibung unterschieden, und es werden folgende Sonderzeichen verwendet:  
>   
>  -   Alle Leerzeichen in der URL-Zeichenfolge werden entsprechend den URL-Codierungsstandards durch die Zeichen "%20" ersetzt.  
> -   Ein Leerzeichen im Parameterteil der URL wird durch ein Pluszeichen (+) ersetzt.  
> -   Ein Semikolon in einem beliebigen Teil der Zeichenfolge wird durch die Zeichen "%3A" ersetzt.  
> -   Die Browser sollten die richtige URL-Codierung automatisch ausführen. Sie müssen keines der Zeichen manuell codieren.  
  
 Verwenden Sie die folgende Syntax, um einen Berichtsparameter innerhalb einer URL festzulegen:  
  
```  
  
parameter=value  
```  
  
 Damit Sie beispielsweise die zwei Parameter "ReportMonth" und "ReportYear" angeben können, die in einem Bericht definiert wurden, verwenden Sie die folgende URL für einen Berichtsserver im einheitlichen Modus:  
  
```  
http://myrshost/ReportServer?/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2&ReportMonth=3&ReportYear=2008  
```  
  
 Um beispielsweise dieselben beiden in einem Bericht definierten Parameter anzugeben, verwenden Sie die folgende URL für einen Berichtsserver im integrierten SharePoint-Modus. Beachten Sie `/_vti_bin`:  
  
```  
http://myspsite/subsite/_vti_bin/reportserver?http://myspsite/subsite/AdventureWorks 2008R2/Employee_Sales_Summary_2008R2.rdl&ReportMonth=3&ReportYear=2008  
```  
  
 Verwenden Sie die folgende Syntax, um einen NULL-Wert für einen Parameter zu übergeben:  
  
```  
  
parameter  
:isnull=true  
  
```  
  
 Beispiel:  
  
```  
SalesOrderNumber:isnull=true  
```  
  
 Um einen **Boolean** -Wert zu übergeben, verwenden Sie 0 für "false" und 1 für "true". Um einen **Float** -Wert zu übergeben, schließen Sie das Dezimaltrennzeichen des Servergebietsschemas ein  
  
> [!NOTE]  
>  Wenn Ihr Bericht einen Berichtsparameter enthält, der einen Standardwert besitzt, und der Wert der **Prompt** -Eigenschaft **FALSE** ist (dies bedeutet, dass die PromptUser-Eigenschaft im Berichts-Manager nicht ausgewählt ist), können Sie keinen Wert für diesen Berichtsparameter innerhalb einer URL übergeben. Dies ermöglicht Administratoren, Benutzer daran zu hindern, die Werte bestimmter Berichtsparameter hinzuzufügen oder zu ändern.  
  
##  <a name="bkmk_examples"></a> Zusätzliche Beispiele  
 Die URL im folgenden Beispiel enthält Leerzeichen und mehrere Parameter.  
  
-   Der Ordnername SQL Server User Education Team enthält Leerzeichen; daher wird jedes Leerzeichen durch das Pluszeichen (+) ersetzt.  
  
-   Der Berichtsname Team Project Report enthält Leerzeichen, und daher wird jedes Leerzeichen durch das Pluszeichen (+) ersetzt.  
  
-   Übergibt zwei teamgrouping2-Parameter mit dem Wert xgroup und teamgrouping1 mit dem Wert ygroup.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup  
```  
  
 Die URL im folgenden Beispiel enthält einen aus mehreren Werten bestehenden OrderID-Parameter. Das Format für einen aus mehreren Werten bestehenden Parameter legt fest, dass der Parametername für jeden Wert wiederholt wird.  
  
```  
https://myserver/Reportserver?/SQL+Server+User+Education+Team/_ContentTeams/folder123/team+project+report&teamgrouping2=xgroup&teamgrouping1=ygroup&OrderID=747&OrderID=787&OrderID=12  
```  
  
 Im folgenden Beispiel für eine URL wird der einzelne *SellStartDate* -Parameter mit dem Wert „7/1/2005“ für einen Berichtsserver im einheitlichen Modus übergeben.  
  
```  
http://myserver/ReportServer/Pages/ReportViewer.aspx?%2fProduct_and_Sales_Report_AdventureWorks&SellStartDate=7/1/2005  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [URL-Zugriff &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [URL Access Parameter Reference (URL-Zugriffsparameterverweis)](../reporting-services/url-access-parameter-reference.md)  
  
  
