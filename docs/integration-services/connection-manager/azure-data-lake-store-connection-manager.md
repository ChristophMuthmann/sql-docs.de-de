---
title: Azure Data Lake-Speicher-Verbindungs-Manager | Microsoft Docs
ms.custom: 
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
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
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a2e3655bedbb24f2174a62c8792cd168e7642592
ms.openlocfilehash: 39630087acdb2ade2e77d4364e4467f8d740d8d4
ms.contentlocale: de-de
ms.lasthandoff: 08/03/2017

---
# <a name="azure-data-lake-store-connection-manager"></a>Azure Data Lake Store-Verbindungsmanager
  Der **Azure Data Lake Store-Verbindungsmanager** ermöglicht, dass ein SSIS-Paket eine Verbindung mit einem Azure Data Lake Store-Dienst durch zwei Authentifizierungstypen herstellt: Azure AD User Identity und Azure AD Service Identity.  
  
 Die **Azure Data Lake-Speicher-Verbindungs-Manager** ist eine Komponente von der [SQL Server Integration Services (SSIS) Feature Pack für Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Um sicherzustellen, dass der Azure Data Lake Store-Verbindungsmanager und die Komponenten, die ihn verwenden – das bedeutet Azure Data Lake Store Source und Azure Data Lake Store Destination – eine Verbindung zu Diensten herstellen können, stellen Sie sicher, dass Sie die neueste Version von Azure Feature Pack [hier](https://www.microsoft.com/download/details.aspx?id=49492)herunterladen. 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Konfigurieren des Azure Data Lake Store-Verbindungs-Manager

 
1.  Wählen Sie im Dialogfeld **SSIS-Verbindungs-Manager hinzufügen** die Option **AzureDataLake**aus, und klicken Sie auf **Hinzufügen**.  
  
2.  Geben Sie im Dialogfeld Azure Data Lake Store-Verbindungsmanager-Editor die URL des Azure Data Lake Store-Host in das Feld **ADLS Host** ein. Zum Beispiel: `https://test.azuredatalakestore.net` oder `test.azuredatalakestore.net`.
  
3.  Wählen Sie den entsprechenden Authentifizierungstyp für den Zugriff auf Azure Data Lake Store-Daten aus.

    1.  Wenn Sie die Option **Azure AD User Identity** ausgewählt haben, führen Sie folgendes aus:
        1. Geben Sie Werte für die Felder **Benutzername** und **Kennwort** an. 
    
        2. Klicken Sie auf die Schaltfläche **Verbindung testen** , um die Verbindung zu testen. Wenn Sie und der Mandantenadministrator vorher nicht zugestimmt haben, dass SSIS auf Azure Data Lake Store-Daten zugreift, müssen Sie auf die Schaltfläche **Annehmen** klicken, um im Popout-Dialog die Zustimmung zu erteilen, dass SSIS auf Ihre Azure Data Lake Store-Daten zugreifen darf. Weitere Informationen über diese Zustimmungsoberfläche finden Sie unter [Integrieren von Anwendungen in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Bei der Authentifizierungsoption „Azure AD User Identity“ werden die mehrstufige Authentifizierung und das Microsoft-Konto NICHT unterstützt.
    
    2. Wenn Sie die Option **Azure AD Service Identity** ausgewählt haben, führen Sie Folgendes durch:
        1. Erstellen Sie eine AAD-Anwendung und ein Dienstprinzipal, die auf Azure Data Lake-Ressourcen zugreifen können.
    
        2. Weisen Sie dieser AAD-Anwendung die entsprechenden Berechtigungen zu, um auf Ihre Azure Data Lake-Ressourcen zuzugreifen. Weitere Informationen zu dieser Authentifizierungsoption finden Sie unter [Use portal to create Active Directory application and service principal that can access resources (Verwenden von Portal zum Erstellen von Active Directory-Anwendungen und Dienstprinzipal zum Zugriff auf Ressourcen)](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Geben Sie Werte für die Felder **Client-ID**, **Geheimer Schlüssel** , und **Mandantenname** an.
    
        4. Klicken Sie auf die Schaltfläche **Verbindung testen** , um die Verbindung zu testen.  
  
6.  Klicken Sie auf **OK** , um das Dialogfeld zu schließen.  
  
    Die Eigenschaften des Verbindungs-Managers, die Sie im Fenster **Eigenschaften** erstellt haben, werden angezeigt.  
  
  
