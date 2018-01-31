---
title: Azure Data Lake Store-Verbindungs-Manager | Microsoft-Dokumentation
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9d98d6cf214a4d08e3a617ab19307bfd42b58189
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store-Verbindungsmanager
Ein SSIS-Paket (SQL Server Integration Services) kann den Azure Data Lake Store-Verbindungs-Manager verwenden, um einen Azure Data Lake Store-Dienst mit einem der beiden folgenden Authentifizierungstypen zu verbinden:
-   Azure AD-Benutzeridentität
-   Azure AD-Dienstidentität 

Der Azure Data Lake Store-Verbindungs-Manager ist eine Komponente von [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Um sicherzustellen, dass der Azure Data Lake Store-Verbindungsmanager und die Komponenten, die ihn verwenden – das bedeutet Azure Data Lake Store Source und Azure Data Lake Store Destination – eine Verbindung zu Diensten herstellen können, stellen Sie sicher, dass Sie die neueste Version von Azure Feature Pack [hier](https://www.microsoft.com/download/details.aspx?id=49492)herunterladen. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Konfigurieren des Azure Data Lake Store-Verbindungs-Manager

1.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** **AzureDataLake** aus, und klicken Sie auf **Hinzufügen**. Das Dialogfeld **Azure Data Lake Store Connection Manager Editor** (Azure Data Lake Store-Verbindungs-Manager-Editor) wird geöffnet.
  
2.  Geben Sie im Dialogfeld **Azure Data Lake Store Connection Manager Editor** (Azure Data Lake Store-Verbindungs-Manager-Editor) im Feld **ADLS Host** (ADLS-Host) die URL des Azure Data Lake Store-Hosts ein. Zum Beispiel: `https://test.azuredatalakestore.net` oder `test.azuredatalakestore.net`.
  
3.  Wählen Sie im Feld **Authentifizierung** den entsprechenden Authentifizierungstyp für den Zugriff auf Daten in Azure Data Lake Store aus.

    1.  Wenn Sie die Authentifizierungsoption **Azure AD-Benutzeridentität** ausgewählt haben, gehen Sie wie folgt vor:
        1. Geben Sie Werte für die Felder **Benutzername** und **Kennwort** an. 
    
        2. Klicken Sie auf **Verbindung testen**, um die Verbindung zu testen. Wenn Sie oder der Mandantenadministrator dem Zugriff von SSIS auf Ihre Azure Data Lake Store-Daten nicht zugestimmt haben, klicken Sie bei Aufforderung auf **Accept** (Zustimmen). Weitere Informationen über diese Zustimmungsoberfläche finden Sie unter [Integrieren von Anwendungen in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Bei Auswahl der Authentifizierungsoption **Azure AD-Benutzeridentität** werden die mehrstufige Authentifizierung und die Authentifizierung mittels Microsoft-Konto nicht unterstützt.
    
    2. Wenn Sie die Option **Azure AD Service Identity** (Azure AD-Dienstidentität) ausgewählt haben, gehen Sie wie folgt vor:
        1. Erstellen Sie eine AAD-Anwendung (Azure Active Directory) und einen Dienstprinzipal für den Zugriff auf Daten in Azure Data Lake.
    
        2. Weisen Sie der AAD-Anwendung die entsprechenden Berechtigungen zu, damit diese auf Ihre Azure Data Lake-Ressourcen zugreifen kann. Weitere Informationen zu dieser Authentifizierungsoption finden Sie unter [Use portal to create Active Directory application and service principal that can access resources (Verwenden von Portal zum Erstellen von Active Directory-Anwendungen und Dienstprinzipal zum Zugriff auf Ressourcen)](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Geben Sie Werte für die Felder **Client-ID**, **Geheimer Schlüssel** und **Mandantenname** an.
    
        4. Klicken Sie auf **Verbindung testen**, um die Verbindung zu testen.  
  
6.  Klicken Sie auf **OK**, um das Dialogfeld **Azure Data Lake Store Connection Manager Editor** (Azure Data Lake Store-Verbindungs-Manager-Editor) zu schließen.  

## <a name="view-the-properties-of-the-connection-manager"></a>Anzeigen der Eigenschaften des Verbindungs-Managers
Die Eigenschaften des Verbindungs-Managers, die Sie im Fenster **Eigenschaften** erstellt haben, werden angezeigt.  
  
  
