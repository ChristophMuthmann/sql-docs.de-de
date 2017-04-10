---
title: "Anmelden an einer Instanz von SQL Server (Befehlszeile) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Anmeldungen [SQL Server], benannte Instanz von SQL Server"
  - "Anmeldungen [SQL Server]"
  - "Anmeldungen [SQL Server], Standardinstanz von SQL Server"
  - "Eingabeaufforderung [SQL Server], Anmeldungen"
  - "Anmelden [SQL Server]"
ms.assetid: f67c11e3-c519-40c9-82c1-07efa9d9985e
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# Anmelden an einer Instanz von SQL Server (Befehlszeile)
  In diesem Thema wird beschrieben, wie Sie die Konnektivität mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mithilfe des Hilfsprogramms **sqlcmd** testen.  
  
##  <a name="SSMSProcedure"></a>  
  
#### So melden Sie sich an der Standardinstanz von SQL Server an  
  
1.  Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, um eine Verbindung mithilfe der Windows-Authentifizierung herzustellen:  
  
    ```  
    sqlcmd [ /E ] [ /S servername ]  
  
    ```  
  
#### So melden Sie sich an einer benannten Instanz von SQL Server an  
  
1.  Geben Sie an einer Eingabeaufforderung den folgenden Befehl ein, um eine Verbindung mithilfe der Windows-Authentifizierung herzustellen:  
  
    ```  
    sqlcmd [ /E ] /S servername\instancename  
  
    ```  
  
## Siehe auch  
 [sqlcmd (Hilfsprogramm)](../../tools/sqlcmd-utility.md)   
 [osql (Hilfsprogramm)](../../tools/osql-utility.md)  
  
  