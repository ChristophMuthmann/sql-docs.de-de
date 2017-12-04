---
title: Suchen der Berichtsdefinitions-Schemaversion (SSRS) | Microsoft-Dokumentation
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML schemas [Reporting Services]
- Report Definition Language, XML schema
- schemas [Reporting Services]
ms.assetid: 67954419-1b61-4481-a3b9-23b4ba7a5624
caps.latest.revision: "15"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: dadc45cb80ec7fa1fedca54af2a17eef5eef2bf6
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/09/2017
---
# <a name="find-the-report-definition-schema-version-ssrs"></a>Suchen der Berichtsdefinitions-Schemaversion (SSRS)

In einer Berichtsdefinitionsdatei ist der RDL-Namespace für die Version des Berichtsdefinitionsschemas angegeben, das zur Überprüfung der RDL-Datei verwendet wird. Wenn Sie eine RDL-Datei in einer Berichterstellungsumgebung wie dem Berichts-Designer in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] oder dem Berichts-Generator öffnen und der Bericht für einen vorherigen Namespace erstellt wurde, wird automatisch eine Sicherungsdatei erstellt und der Bericht auf den aktuellen Namespace aktualisiert. Wenn Sie die aktualisierte Berichtsdefinition speichern, haben Sie die konvertierte RDL-Datei gespeichert. Dies ist die einzige Möglichkeit, eine Berichtsdefinition zu aktualisieren. Die Berichtsdefinition selbst wird auf einem Berichtsserver nicht aktualisiert. Der kompilierte Bericht wird auf einem Berichtsserver aktualisiert. Weitere Informationen finden Sie unter [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  
  
### <a name="how-to-identify-the-rdl-schema-version-of-a-report"></a>Vorgehensweise: Identifizieren der RDL-Schemaversion eines Berichts  
  
1.  Öffnen Sie die RDL-Berichtsdatei in einer Anwendung wie dem Editor oder XML Notepad 2007, in der Sie XML anzeigen können.  
  
     Das XML-Berichtselement gibt den Schemanamespace an. Zum Beispiel gibt das folgende Berichtselement den Namespace für den Berichts-Designer und den Namespace für die Berichtsdefinition an.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Der Berichtsdefinitionsnamespace wird von der folgenden URL angegeben: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`.  
  
### <a name="how-to-identify-the-rdl-schema-version-of-report-designer"></a>Vorgehensweise: Identifizieren der RDL-Schemaversion des Berichts-Designers  
  
1.  Öffnen Sie ein neues Projekt. Die Version des ausgewählten Projekts bestimmt die Version des RDL-Schemas. In SQL Server werden mehrere Schemaversionen unterstützt. Weitere Informationen finden Sie unter [Bereitstellung und Versionsunterstützung in SQL Server Data Tools](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
2.  Klicken Sie im Menü **Projekt** auf **Neues Element hinzufügen**. Das Dialogfeld **Neues Element hinzufügen** wird geöffnet.  
  
3.  Klicken Sie im Bereich **Vorlagen** auf **Bericht**.  
  
4.  Geben Sie im Feld **Name**einen Berichtsnamen ein, oder übernehmen Sie den Standardnamen.  
  
5.  Klicken Sie auf **Hinzufügen**. Der Berichts-Designer öffnet in der Entwurfsansicht einen neuen leeren Bericht.  
  
6.  Klicken Sie im Menü **Ansicht** auf **Code**. Die Berichtsdefinition wird als XML-Datei angezeigt.  
  
     Das XML-Berichtselement gibt den Schemanamespace an. Zum Beispiel gibt das folgende Berichtselement den Namespace für den Berichts-Designer und den Namespace für die Berichtsdefinition an.  
  
    ```  
    <Report xmlns:rd=http://schemas.microsoft.com/SQLServer/reporting/reportdesigner  
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition">  
    ```  
  
     Der Berichtsdefinitionsnamespace wird von der folgenden URL angegeben: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  
  
### <a name="how-to-identify-the-rdl-schema-version-on-the-report-server"></a>Vorgehensweise: Identifizieren der RDL-Schemaversion auf dem Berichtsserver  
  
-   Geben Sie im Berichts-Manager die URL für den Berichtsserver ein. Die folgende URL gibt z. B. einen Berichtsserver auf dem lokalen Computer an:  
  
     `http://localhost/reportserver/reportdefinition.xsd`  
  
     Die XSD-Datei wird im Browser geöffnet.  
  
     Das XML-Schemaelement gibt den Schemanamespace an. Das folgende Schemaelement gibt beispielsweise drei Namespaces an: den targetNamespace-Verweis, der intern von [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]verwendet wird, den XSD-Verweis für das Schema selbst (XSD) und die Berichtsdefinitionsreferenz.  
  
    ```  
    <xsd:schema   
    targetNamespace="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    xmlns:xsd="http://www.w3.org/2001/XMLSchema"   
    xmlns="http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition"   
    elementFormDefault="qualified">  
    ```  
  
     Der Berichtsdefinitionsnamespace wird von der folgenden URL angegeben: `http://schemas.microsoft.com/sqlserver/reporting/2009/01/reportdefinition`  

## <a name="next-steps"></a>Nächste Schritte

[Aktualisieren von Berichten](../../reporting-services/install-windows/upgrade-reports.md)   
[Report Definition Language (Berichtsdefinitionssprache)](../../reporting-services/reports/report-definition-language-ssrs.md)  

Haben Sie dazu Fragen? [Stellen Sie eine Frage im Reporting Services-Forum](http://go.microsoft.com/fwlink/?LinkId=620231)
