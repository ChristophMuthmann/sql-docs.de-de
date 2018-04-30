---
title: Kenntnisse der Unterschiede von Datentypen | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ab8fa00f-cb16-47e2-94b8-3a76f56c2b84
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf10944059322a159de43ccee2a7e4d8ed1d8526
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-data-type-differences"></a>Grundlegendes zu den Unterschieden von Datentypen
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Es gibt eine Reihe von Unterschieden zwischen den Java-Datentypen und [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] -Datentypen. Die [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] verschiedenartige berücksichtigt diese Unterschiede durch verschiedene Typen von Konvertierungen.  
  
## <a name="character-types"></a>Zeichentypen  
 Der JDBC-Zeichenfolgentypen werden **CHAR**, **VARCHAR**, und **LONGVARCHAR**. Der JDBC-Treiber unterstützt die JDBC 4.0-API. In JDBC 4.0 sind auch die JDBC-Zeichenfolgentypen sein können **NCHAR**, **NVARCHAR**, und **LONGNVARCHAR**. Diese neuen Zeichenfolgentypen verwalten die systemeigenen Java-Zeichentypen im Unicode-Format, sodass keine Konvertierung von ANSI nach Unicode und Unicode nach ANSI mehr erforderlich ist.  
  
|Typ|Description|  
|----------|-----------------|  
|Feste Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Char** und **Nchar** Datentypen zugeordnet werden, direkt an den JDBC **CHAR** und **NCHAR** Typen. Diese Typen weisen eine feste Länge auf und werden vom Server mit Leerstellen aufgefüllt, wenn für die Spalte SET ANSI_PADDING ON festgelegt wurde. Auffüllung ist stets eingeschaltet, für **Nchar**, aber für **Char**, im Fall, in dem die Zeichenspalten des Servers nicht aufgefüllt werden, fügt der JDBC-Treiber die Leerstellen.|  
|Variable Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varchar** und **Nvarchar** Typen sind direkt den JDBC **VARCHAR** und **NVARCHAR** bzw. die Argumenttypen.|  
|Long|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Text** und **Ntext** Typen zuordnen, um die JDBC **LONGVARCHAR** und **LONGNVARCHAR** vom Typ. Diese sind als veraltet markierte Typen ab [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], weshalb Sie große Werttypen verwenden sollten **varchar(max)** oder **nvarchar(max)**, stattdessen.<br /><br /> Verwenden das Update\<numerischen Typ > und [UpdateObject (Int, java.lang.Object)](../../connect/jdbc/reference/updateobject-method-int-java-lang-object.md) -Methode treten für **Text** und **Ntext** -Serverspalten. Allerdings mithilfe der [SetObject](../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md) Methode mit einem zeichenkonvertierungstyps wird gegen unterstützt **Text** und **Ntext** -Serverspalten.|  
  
## <a name="binary-string-types"></a>Binäre Zeichenfolgetypen  
 Die binären JDBC-Zeichenfolgentypen werden **BINÄRE**, **VARBINARY**, und **"LONGVARBINARY"**.  
  
|Typ|Description|  
|----------|-----------------|  
|Feste Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **binäre** geben Zuordnungen direkt an den JDBC **BINÄRE** Typ. Dieser Typ weist eine feste Länge auf und wird vom Server mit Leerstellen aufgefüllt, wenn für die Spalte SET ANSI_PADDING ON eingestellt wurde. Wenn die Zeichenspalten des Servers nicht mit Leerstellen aufgefüllt sind, fügt der JDBC-Treiber die Leerstellen hinzu.<br /><br /> Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Zeitstempel** Typ ist ein JDBC **BINÄRE** Typ mit einer festen Länge von 8 Bytes.|  
|Variable Länge|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Varbinary** geben Zuordnungen in der JDBC **VARBINARY** Typ.<br /><br /> Die **Udt** Geben Sie in [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] in JDBC ordnet eine **VARBINARY** Typ.|  
|Long|Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Image** geben Zuordnungen in der JDBC **"LONGVARBINARY"** Typ. Dieser Typ ist ab veraltet [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], sodass Sie einen großen Werttyp aufweist, verwenden sollten **varbinary(max)** stattdessen.|  
  
## <a name="exact-numeric-types"></a>Exakte numerische Typen  
 Die exakten numerischen JDBC-Typen sind direkt den entsprechenden SQL Server-Typen zugeordnet.  
  
|Typ|Description|  
|----------|-----------------|  
|BIT|Der JDBC **BIT** Typ stellt ein einzelnes Bit, die 0 oder 1 sein kann. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Bit** Typ.|  
|TINYINT|Der JDBC **"tinyint"** -Typ stellt ein einzelnes Byte dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"tinyint"** Typ.|  
|SMALLINT|Der JDBC **"smallint"** Typ stellt eine 16-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"smallint"** Typ.|  
|INTEGER|Der JDBC **Ganzzahl** Typ stellt eine 32-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Int** Typ.|  
|bigint|Der JDBC **"bigint"** Typ stellt eine 64-Bit-Ganzzahl mit Vorzeichen dar. Dies ordnet eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"bigint"** Typ.|  
|NUMERIC|Der JDBC **numerischen** Typ stellt einen Dezimalwert fester Genauigkeit, die Werte mit identischer Genauigkeit enthält. Die **numerischen** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **numerischen** Typ.|  
|DECIMAL|Der JDBC **DECIMAL** Typ darstellt, einen fester Genauigkeit Dezimalwert, dass die Werte mit mindestens der angegebenen Genauigkeit enthält. Die **DECIMAL** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **decimal** Typ.<br /><br /> Der JDBC **DECIMAL** Typ ordnet auch die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Money** und **Smallmoney** Typen, die spezielle Dezimaltypen fester Genauigkeit, die in 8 und 4 gespeichert sind Bytes bzw.|  
  
## <a name="approximate-numeric-types"></a>Angenäherte numerische Typen  
 Die angenäherten numerischen JDBC-Typen sind **echte**, **doppelte**, und **FLOAT**.  
  
|Typ|Description|  
|----------|-----------------|  
|real|Der JDBC **echte** Typ weist sieben Ziffern für die Genauigkeit auf (einfache Genauigkeit) und ordnet Sie direkt an die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **echte** Typ.|  
|DOUBLE|Der JDBC **doppelte** Typ weist 15 Ziffern für die Genauigkeit auf (doppelte Genauigkeit) und ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"float"** Typ. Der JDBC **FLOAT** Typ ist ein Synonym für **doppelte**. Da zwischen Verwechslungen **FLOAT** und **doppelte**, **doppelte** wird bevorzugt.|  
  
## <a name="datetime-types"></a>Datum-/Zeittypen  
 Der JDBC **Zeitstempel** Typ ordnet die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **"DateTime"** und **Smalldatetime** Typen. Die **"DateTime"** -Typ wird in zwei 4-Byte-integer-Werten gespeichert. Die **Smalldatetime** Typ enthält die gleichen Informationen (Datum und Uhrzeit), jedoch mit geringerer Genauigkeit in zwei 2-Byte-integer-Werten.  
  
> [!NOTE]  
>  Die [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **Zeitstempel** Typ ist ein binäre Zeichenfolge fester Länge. Es ist nicht an ein beliebiges der JDBC-Typen zugeordnet: **Datum**, **Zeit**, oder **Zeitstempel**.  
  
## <a name="custom-type-mapping"></a>Benutzerdefinierte Typzuordnung  
 Die Zuordnungsfunktion für benutzerdefinierte Typen von JDBC, die die SQLData-Schnittstellen für die JDBC verwendet erweiterte Typen (UDTs, Struct usw.). ist im JDBC-Treiber nicht implementiert.  
  
## <a name="see-also"></a>Siehe auch  
 [Grundlegendes zu den Datentypen in JDBC Driver](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)  
  
  
