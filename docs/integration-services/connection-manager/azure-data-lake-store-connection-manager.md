---
title: Azure Data Lake-Speicher-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: 0a84b10114d785c9216a0902b2eefbcb0bd3f4c8
ms.contentlocale: de-de
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store-Verbindungsmanager
Ein SQL Server Integration Services (SSIS)-Paket kann den Azure Data Lake-Speicher-Verbindungs-Manager verwenden, für die Verbindung mit einer Azure Data Lake-Speicher-Dienst mit einem der beiden folgenden Authentifizierungstypen:
-   Azure AD-Benutzeridentität
-   Azure AD-Dienstidentität 

Der Azure Data Lake-Speicher-Verbindungs-Manager ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Um sicherzustellen, dass der Azure Data Lake Store-Verbindungsmanager und die Komponenten, die ihn verwenden – das bedeutet Azure Data Lake Store Source und Azure Data Lake Store Destination – eine Verbindung zu Diensten herstellen können, stellen Sie sicher, dass Sie die neueste Version von Azure Feature Pack [hier](https://www.microsoft.com/download/details.aspx?id=49492)herunterladen. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Konfigurieren des Azure Data Lake Store-Verbindungs-Manager

1.  In der **SSIS-Verbindungs-Manager hinzufügen** wählen Sie im Dialogfeld **AzureDataLake**, und wählen Sie dann **hinzufügen**. Die **Azure Data Lake-Speicher-Verbindungs-Manager-Editor** Dialogfeld wird geöffnet.
  
2.  In der **Azure Data Lake-Speicher-Verbindungs-Manager-Editor** Dialogfeld die **ADLS Host** Feld, geben Sie die URL der Azure Data Lake-Speicher-Host. Zum Beispiel: `https://test.azuredatalakestore.net` oder `test.azuredatalakestore.net`.
  
3.  In der **Authentifizierung** Feld, und wählen Sie den entsprechenden Authentifizierungstyp für den Datenzugriff in Azure Data Lake-Speicher.

    1.  Bei Auswahl der **Azure AD-Benutzeridentität** Authentifizierung aktivieren, führen Sie folgende Schritte aus:
        1. Geben Sie Werte für die **Benutzername** und **Kennwort** Felder. 
    
        2. Wählen Sie zum Testen der Verbindung **Verbindung testen**. Wenn Sie oder der mandantenadministrator zuvor stimmen nicht SSIS wählen, um den Zugriff auf Ihre Azure Data Lake-Speicher-Daten zulassen **Accept** Aufforderung. Weitere Informationen über diese Zustimmungsoberfläche finden Sie unter [Integrieren von Anwendungen in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Bei Auswahl der **Azure AD-Benutzeridentität** Authentifizierungsoption, mehrstufige Authentifizierung und Authentifizierung der Microsoft-Konto werden nicht unterstützt.
    
    2. Bei Auswahl der **Azure AD-Dienstidentität** Authentifizierung aktivieren, führen Sie folgende Schritte aus:
        1. Erstellen Sie ein Azure Active Directory (AAD)-Anwendung und Dienst Dienstprinzipalnamen für den Azure Data Lake-Datenzugriff.
    
        2. Weisen Sie die erforderlichen Berechtigungen für diese AAD-Anwendung, die Ihre Azure Data Lake-Ressourcen zugreifen können. Weitere Informationen zu dieser Authentifizierungsoption finden Sie unter [Use portal to create Active Directory application and service principal that can access resources (Verwenden von Portal zum Erstellen von Active Directory-Anwendungen und Dienstprinzipal zum Zugriff auf Ressourcen)](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Geben Sie Werte für die **Clientkennung**, **Geheimschlüssel**, und **Mandantenname** Felder.
    
        4. Wählen Sie zum Testen der Verbindung **Verbindung testen**.  
  
6.  Wählen Sie **OK** schließen die **Azure Data Lake-Speicher-Verbindungs-Manager-Editor** (Dialogfeld).  

## <a name="view-the-properties-of-the-connection-manager"></a>Zeigen Sie die Eigenschaften des Verbindungs-Managers
Die Eigenschaften des Verbindungs-Managers, die Sie im Fenster **Eigenschaften** erstellt haben, werden angezeigt.  
  
  
