---
title: "Geschäftsregelerweiterung (Master Data Services) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4c18be5f-a3fa-45a8-9be6-0f45f58bbc9e
caps.latest.revision: 16
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: e83f09094cde9a2643913fceae32d1f6a07a7c09
ms.contentlocale: de-de
ms.lasthandoff: 09/07/2017

---
# <a name="business-rules-extension-master-data-services"></a>Geschäftsregelerweiterung (Master Data Services)
  Sie können in [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]benutzerdefinierte SQL-Skripts als Erweiterung vordefinierter Bedingungen und Aktionen anwenden.  
  
> [!NOTE]  
>  Alle Skripts müssen unter dem Schema „[usr]“ definiert werden.  
  
 SQL-Funktionen, die die folgenden Kriterien erfüllen, können als Geschäftsregelbedingung verwendet werden.  
  
-   Der Typ des Rückgabewerts muss BIT sein.  
  
-   Nur die folgenden Typen werden als Parametertypen unterstützt.  
  
    -   NVARCHAR  
  
    -   DATETIME2  
  
    -   DECIMAL (Genauigkeit, Dezimalstellen)  
  
         Der Wert für die Genauigkeit muss 38 betragen.  
  
         Der Dezimalstellenwert muss in einem Bereich zwischen 0 und 7 liegen.  
  
 Gespeicherte SQL-Prozeduren mit der folgenden Syntax können als Geschäftsregelaktion verwendet werden.  
  
```  
CREATE PROCEDURE [usr].[YourAction]  
       (         
            @MemberIdList mdm.[MemberId] READONLY,  
            @ModelName NVARCHAR(MAX),  
            @VersionName NVARCHAR(MAX),  
            @EntityName NVARCHAR(MAX),  
            @BusinessRuleName NVARCHAR(MAX)  
        )    
      AS BEGIN    
       ...     
       END  
  
```  
  
 Bereitstellungspaketen werden keine benutzerdefinierten Skripts hinzugefügt. Stellen Sie vor dem Bereitstellen eines Pakets sicher, dass die Master Data Services-Zieldatenbank alle Skripts enthält, die in den Geschäftsregeln verwendet werden.  
  
 Skriptaktionen werden als „mds_br_user“ ausgeführt, der über die folgenden Berechtigungen verfügt.  
  
|||  
|-|-|  
|**Schema**|**Berechtigungen**|  
|mdm|SELECT|  
|stg|SELECT, UPDATE, DELETE, EXECUTE, INSERT|  
|usr|FULL|  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
 So führen Sie diese Prozedur aus  
  
-   Sie müssen über die Berechtigung verfügen, auf den Funktionsbereich "Systemverwaltung" zuzugreifen.  
  
-   Sie müssen ein Modelladministrator sein. Weitere Informationen finden Sie unter [Administratoren &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)  
  
-   Der [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]-Datenbank wurden benutzerdefinierte Skripts hinzugefügt.  
  
## <a name="create-a-business-rule-to-take-a-user-defined-script-as-a-condition-or-as-an-action"></a>Erstellen Sie eine Geschäftsregel, um ein benutzerdefiniertes Skript als Bedingung oder Aktion zu verwenden.  
  
1.  Klicken Sie im Master Data Manager auf **Systemverwaltung**.  
  
2.  Zeigen Sie auf der Menüleiste auf **Verwalten** , und klicken Sie auf **Geschäftsregeln**.  
  
3.  Wählen Sie in der Dropdownliste **Modell** auf der Seite **Geschäftsregeln** ein Modell aus.  
  
4.  Wählen Sie in der Dropdownliste **Entität** eine Entität aus.  
  
5.  Wählen Sie aus der Dropdownliste **Elementtyp** einen Typ des Elements aus, auf das die Geschäftsregel angewendet werden soll.  
  
6.  Klicken Sie auf **Hinzufügen**.  
  
7.  Gehen Sie wie folgt vor, um ein benutzerdefiniertes Skript als Bedingung zu erstellen.  
  
    1.  Klicken Sie unter dem **IF** -Abschnitt auf die Schaltfläche **Hinzufügen** . Ein Panel wird angezeigt.  
  
    2.  Wählen Sie in der Dropdownliste **Operator** unter **Benutzerdefiniertes Skript** die benutzerdefinierte Funktion aus.  
  
    3.  Alle Parameter der benutzerdefinierten Funktion werden angezeigt.  
  
    4.  Weisen Sie jedem Parameter einen Wert zu.  
  
    5.  Klicken Sie auf **Speichern**.  
  
8.  Gehen Sie wie folgt vor, um ein benutzerdefiniertes Skript als Aktion zu verwenden.  
  
    1.  Klicken Sie unter dem **THEN** -Abschnitt auf die Schaltfläche **Hinzufügen** . Ein Panel wird angezeigt.  
  
    2.  Wählen Sie in der Dropdownliste **Operator** unter **Benutzerdefiniertes Skript** eine benutzerdefinierte Funktion aus.  
  
    3.  Klicken Sie auf **Speichern**.  
  
## <a name="see-also"></a>Siehe auch  
 [Geschäftsregeln &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Geschäftsregelbedingungen &#40;Master Data Services&#41;](../master-data-services/business-rule-conditions-master-data-services.md)   
 [Geschäftsregelaktionen &#40;Master Data Services&#41;](../master-data-services/business-rule-actions-master-data-services.md)  
  
  

