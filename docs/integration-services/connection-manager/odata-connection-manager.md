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
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: b23a158bff546fd6ffb4208638c039d690379ce1
ms.contentlocale: de-de
ms.lasthandoff: 08/09/2017

---
# <a name="odata-connection-manager"></a>OData-Verbindungs-Manager
  Verwenden Sie einen OData-Verbindungs-Manager zum Herstellen einer Verbindung mit einer OData-Quelle. Eine OData-Quellkomponente stellt über einen OData-Verbindungs-Manager eine Verbindung mit einer OData-Quelle her und verwendet die Daten des Diensts. Weitere Informationen finden Sie unter [OData Source](../../integration-services/data-flow/odata-source.md).  
  
## <a name="adding-an-odata-connection-manager-to-an-ssis-package"></a>Hinzufügen eines OData-Verbindungs-Managers zu einem SSIS-Paket  
 Sie können einem SSIS-Paket einen neuen OData-Verbindungs-Manager auf drei Arten hinzufügen:  
  
-   Klicken Sie im **Quellen-Editor für OData** auf die Schaltfläche **Neu**  
  
-   Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf den Ordner **Verbindungs-Manager**, und klicken Sie anschließend auf **Neuer Verbindungs-Manager**. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
-   Klicken Sie unten im Paket-Designer mit der rechten Maustaste auf **Verbindungs-Manager** , und wählen Sie **Neue Verbindung**aus. Wählen Sie unter **Typ des Verbindungs-Managers** die Option **ODATA**aus.  
  
## <a name="connection-manager-authentication"></a>Verbindungs-Manager-Authentifizierung  
 Der OData-Verbindungs-Manager unterstützt fünf Authentifizierungsmodi.  
  
-   Windows-Authentifizierung  
  
-   Standardauthentifizierung (mit Benutzername und Kennwort)  

-   Microsoft Dynamics AX Online (mit Benutzername und Kennwort)
  
-   Microsoft Dynamics CRM Online (mit Benutzername und Kennwort)
  
-   Microsoft Online Services (mit Benutzername und Kennwort)  
  
 Für den anonymen Zugriff wählen Sie die Option „Windows-Authentifizierung“ aus.  
  
### <a name="specifying-and-securing-credentials"></a>Festlegen und Sichern von Anmeldeinformationen  
 Wenn der OData-Dienst die Standardauthentifizierung erfordert, können Sie im [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)einen Benutzernamen und ein Kennwort angeben. Die Werte, die Sie in den Editor eingeben, werden im Paket beibehalten. Der Kennwortwert wird gemäß der Schutzebene des Pakets verschlüsselt.  
  
 Es gibt mehrere Möglichkeiten, die Werte für Benutzername und Kennwort zu parametrisieren oder außerhalb des Pakets gespeichert. Beispielsweise können Sie dazu Parameter verwenden oder die Eigenschaften des Verbindungs-Managers beim Ausführen des Pakets in SQL Server Management Studio direkt festlegen.  
  
## <a name="odata-connection-manager-properties"></a>Eigenschaften des OData-Verbindungs-Managers  
 In der folgenden Liste werden die Eigenschaften des OData-Verbindungs-Managers beschrieben.  
  
|||  
|-|-|  
|Eigenschaft|Description|  
|URL|Die URL zum Dienstdokument.|  
|UserName|Der Benutzername, der für die Standardauthentifizierung verwendet wird.|  
|Kennwort|Das Kennwort, das für die Standardauthentifizierung verwendet wird.|  
|ConnectionString|Stellt weitere Eigenschaften des Verbindungs-Managers dar.|  
  
## <a name="odata-connection-manager-editor"></a>OData-Verbindungs-Manager-Editor
  Verwenden Sie das Dialogfeld **OData-Verbindungs-Manager-Editor** , um eine Verbindung hinzufügen oder eine vorhandene Verbindung mit einer OData-Quelle zu bearbeiten.  
  
### <a name="options"></a>enthalten  
 **Name des Verbindungs-Managers**  
 Name des Verbindungs-Managers.  
  
 **Speicherort des Dienstdokuments**  
 URL für den OData-Dienst. Beispiel: http://services.odata.org/V3/Northwind/Northwind.svc/.  
  
 **Authentifizierung**  
 Wählen Sie entweder **Windows-Authentifizierung** oder **Diesen Benutzernamen und dieses Kennwort verwenden** für **Standardauthentifizierung**aus. Wenn Sie die zweite Option auswählen, geben Sie **Benutzername** und **Kennwort**ein. 
 
 Es gibt jetzt drei weitere Optionen. Wählen Sie **Microsoft Dynamics AX Online** für Dynamics AX Online aus, wählen Sie **Microsoft Dynamics CRM Online** für Dynamics CRM Online, und wählen Sie anschließend **Microsoft Online Services** für Microsoft Online Services. Wenn Sie eine der folgenden drei Optionen auswählen, geben Sie den **Benutzernamen** und das **Kennwort**an.
  
 **Verbindung testen**  
 Klicken Sie auf diese Schaltfläche, um die Verbindung mit der OData-Quelle zu testen.  
  
## <a name="see-also"></a>Siehe auch  
 [OData Connection Manager Editor](../../integration-services/connection-manager/odata-connection-manager-editor.md)  
  
  
