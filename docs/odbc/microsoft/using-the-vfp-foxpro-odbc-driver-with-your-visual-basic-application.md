---
title: Verwenden Sie den VFP FoxPro ODBC-Treiber mit Visual Basic-Anwendung | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 37834afc7cc69e0276645d68752e66f68449fbb3
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Verwenden des VFP FoxPro ODBC-Treibers mit Visual Basic-Anwendung
Ihr Microsoft® Visual Basic®-Anwendung kann kommunizieren mit Visual FoxPro-Daten erstellen ein Steuerelement, das mit einer Visual FoxPro-Datenquelle eine Verbindung herstellt.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Verbindung mit Visual FoxPro-Daten über das Steuerelement in Visual Basic  
  
1.  Erstellen Sie eine Datenquelle mit dem Namen "test" die Herstellung der TasTrade-Beispieldatenbank, die im Visual FoxPro enthalten. Die Visual FoxPro-Standardinstallation platziert die Beispieldatenbank TasTrade am Speicherort:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  Erstellen Sie in Visual Basic ein neues Formular, und platzieren Sie ein Textfeld und ein Steuerelement auf.  
  
3.  Ändern Sie die Connect-Eigenschaft des Steuerelements wie folgt:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Ändern der Eigenschaft Recordsettyp wie folgt:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Ändern Sie die Datenherkunft-Eigenschaft, um die folgenden:  
  
    ```  
    customer  
    ```  
  
6.  Ändern Sie die DataSource-Eigenschaft für das Textfeld in der Standardname für das Steuerelement die folgenden:  
  
    ```  
    data1  
    ```  
  
7.  Ändern Sie DataField-Eigenschaft des Textfelds in der folgenden:  
  
    ```  
    customer_id  
    ```  
  
8.  Führen Sie das Formular, und verwenden Sie das Steuerelement über die Kunden-Id-Felder aus der Visual FoxPro-TasTrade-Beispieldatenbank zu überspringen.

