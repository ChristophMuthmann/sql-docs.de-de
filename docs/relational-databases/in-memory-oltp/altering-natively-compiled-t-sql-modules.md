---
title: "&#196;ndern von nativ kompilierten T-SQL-Modulen | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine-imoltp"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
caps.latest.revision: 7
author: "sabotta"
ms.author: "carlasab"
manager: "jhubbard"
caps.handback.revision: 7
---
# &#196;ndern von nativ kompilierten T-SQL-Modulen
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  In [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (und höher) und [!INCLUDE[ssSDS](../../includes/sssds-md.md)] können Sie die ALTER-Vorgänge für nativ kompilierte gespeicherte Prozeduren und andere nativ kompilierte T-SQL-Module, z.B. skalare benutzerdefinierte Funktionen und Trigger, mithilfe der ALTER-Anweisung ausführen.  
  
 Bei der Ausführung von ALTER an einem nativ kompilierten T-SQL-Modul, wird das Modul mit einer neuen Definition neu kompiliert. Während der Neukompilierung steht die alte Version des Moduls nach wie vor noch für die Ausführung zur Verfügung. Nach Abschluss der Kompilierung werden die Modulausführungen entladen und die neue Version des Moduls wird installiert. Die Änderung einer nativ kompilierten T-SQL-Moduls schließt folgende Optionen ein.  
  
-   Parameter  
  
-   EXECUTE AS  
  
-   TRANSACTION ISOLATION LEVEL  
  
-   LANGUAGE  
  
-   DATEFIRST  
  
-   DATEFORMAT  
  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
>  Nativ kompilierte T-SQL-Module können nicht in nicht-nativ kompilierte Module konvertiert werden. Nicht-nativ kompilierte T-SQL-Module können nicht in nativ kompilierte Module konvertiert werden.  
  
 Weitere Informationen zu ALTER PROCEDURE-Funktionen und deren Syntax finden Sie unter [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md).  
  
 Sie können „sp_recompile“ für ein nativ kompiliertes T-SQL-Modul ausführen, wodurch das Modul bei der nächsten Ausführung erneut kompiliert.  
  
## Beispiel  
 Das folgende Beispiel zeigt die Erstellung einer speicheroptimierten Tabelle (T1) und einer systemintern kompilierten gespeicherten Prozedur (SP1), die alle Spalten von Tabelle T1 auswählt. Anschließend wird SP1 geändert, um die Klausel EXECUTE AS zu entfernen, LANGUAGE zu ändern und nur eine Spalte (C1) von T1 auszuwählen.  
  
```  
CREATE TABLE [dbo].[T1]  
(  
[c1] [int] NOT NULL,  
[c2] [float] NOT NULL,  
CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
)WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
 SELECT c1, c2 from dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
 SELECT c1 from dbo.T1  
END  
GO  
  
```  
  
  