---
title: OData-Verbindungs-Manager | Microsoft Docs
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3caa4372-aff3-4c0f-9ecd-97870948b8d0
caps.latest.revision: 9
f1_keywords:
- sql13.dts.designer.odatasource.connectionmanager.f1
- sql13.dts.designer.odataconnectionmanager.f1
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: f54562b59e8c61f723c17e2812ca39cb2e95f273
ms.contentlocale: de-de
ms.lasthandoff: 08/28/2017

---
# <a name="odata-connection-manager"></a>OData-Verbindungs-Manager
 Verbinden Sie mit einer OData-Datenquelle mit einer OData-Verbindungs-Manager. OData-Quellkomponente verwendet einen OData-Verbindungs-Manager zum Herstellen einer Verbindung mit einer OData-Datenquelle und Nutzen von Daten aus dem Dienst. Weitere Informationen finden Sie unter [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Hinzufügen eines OData-Verbindungs-Managers zu einem SSIS-Paket  
 Sie können einen neuen OData-Verbindungs-Manager auf einem SSIS-Paket auf drei Arten hinzufügen:  
  
-   Klicken Sie im **Quellen-Editor für OData** auf die Schaltfläche **Neu**  
  
-   Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Verbindungs-Manager**, und klicken Sie anschließend auf **Neuer Verbindungs-Manager**. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
-   Mit der rechten Maustaste die **Verbindungs-Manager** Bereich am unteren Rand der Paket-Designer, und wählen Sie dann **neue Verbindung**. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
## <a name="connection-manager-authentication"></a>Verbindungs-Manager-Authentifizierung  
 Der OData-Verbindungs-Manager unterstützt fünf Authentifizierungsmodi.  
  
-   Windows-Authentifizierung  
  
-   Standardauthentifizierung (mit Benutzername und Kennwort)  

-   Microsoft Dynamics AX Online (mit Benutzername und Kennwort)
  
-   Microsoft Dynamics CRM Online (mit Benutzername und Kennwort)
  
-   Microsoft Online Services (mit Benutzername und Kennwort)  
  
Für den anonymen Zugriff wählen Sie die Option „Windows-Authentifizierung“ aus.  

Um mit Microsoft Dynamics AX Online oder Microsoft Dynamics CRM online zu verbinden, können Sie keine der **Microsoft Online Services** Authentifizierungsoption. Sie können keine Option, die so konfiguriert ist, auch verwenden, Multi-Factor Authentication.
  
### <a name="specifying-and-securing-credentials"></a>Festlegen und Sichern von Anmeldeinformationen  
 Wenn der OData-Dienst die Standardauthentifizierung erfordert, können Sie im [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)einen Benutzernamen und ein Kennwort angeben. Die Werte, die Sie in den Editor eingeben, werden im Paket beibehalten. Der Kennwortwert wird gemäß der Schutzebene des Pakets verschlüsselt.  
  
 Es gibt mehrere Möglichkeiten, die Werte für Benutzername und Kennwort zu parametrisieren oder außerhalb des Pakets gespeichert. Beispielsweise können Sie Parameter verwenden oder den Verbindungs-Manager-Eigenschaften direkt festgelegt beim Ausführen des Pakets in SQL Server Management Studio.  
  
## <a name="odata-connection-manager-properties"></a>Eigenschaften des OData-Verbindungs-Managers  
 Die folgende Liste beschreibt die Eigenschaften des OData-Verbindungs-Managers.  
  
|||  
|-|-|  
|Eigenschaft|Description|  
|URL|Die URL zum Dienstdokument.|  
|UserName|Der Benutzername für die Authentifizierung verwenden, falls erforderlich.|  
|Kennwort|Kennwort, das zur Authentifizierung zu verwenden, falls erforderlich.|  
|ConnectionString|Schließt andere Eigenschaften des Verbindungs-Managers.|  
  
## <a name="odata-connection-manager-editor"></a>OData-Verbindungs-Manager-Editor
  Verwenden der **OData-Verbindungs-Manager-Editor** (Dialogfeld), um eine Verbindung hinzufügen oder bearbeiten eine vorhandene Verbindung mit einer OData-Datenquelle.  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Name des Verbindungs-Managers.  
  
 **Speicherort des Dienstdokuments**  
 URL für den OData-Dienst. Beispiel: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Authentifizierung**  
Wählen Sie eine der folgenden Optionen aus:
-   **Windows-Authentifizierung**. Wählen Sie diese Option aus, für den anonymen Zugriff.
-   **Standardauthentifizierung** 
-   **Microsoft Dynamics AX Online** für Dynamics AX Online
-   **Microsoft Dynamics CRM Online** für Dynamics CRM Online
-   **Microsoft Online Services** für Microsoft Online Services

Wenn Sie eine Option aus, als die Windows-Authentifizierung auswählen, geben Sie die **Benutzername** und **Kennwort**. 

Um mit Microsoft Dynamics AX Online oder Microsoft Dynamics CRM online zu verbinden, können Sie keine der **Microsoft Online Services** Authentifizierungsoption. Sie können keine Option, die so konfiguriert ist, auch verwenden, Multi-Factor Authentication.

 **Verbindung testen**  
 Klicken Sie auf diese Schaltfläche, um die Verbindung mit der OData-Quelle zu testen.  

