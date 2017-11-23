---
title: Parameter (ADO - WFC-Syntax) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords: Parameter collection [ADO], ADO/WFC syntax
ms.assetid: d00d1e1e-14b1-41a2-a00f-2a3cb7396f15
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac7887cc1e27f1a024ca2332d7a8d413a996f355
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/17/2017
---
# <a name="parameter-ado---wfc-syntax"></a>Parameter (ADO - WFC-Syntax)
## <a name="package-commswfcdata"></a>Paket com.ms.wfc.data  
  
### <a name="constructor"></a>Konstruktor  
  
```  
public Parameter()  
public Parameter(String name)  
public Parameter(String name, int type)  
public Parameter(String name, int type, int dir)  
public Parameter(String name, int type, int dir, int size)  
public Parameter(String name, int type, int dir, int size, Object value)  
```  
  
### <a name="methods"></a>Methoden  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
public int getAttributes()  
public void setAttributes(int attr)  
public int getDirection()  
public void setDirection(int dir)  
public String getName()  
public void setName(String name)  
public int getNumericScale()  
public void setNumericScale(int scale)  
public int getPrecision()  
public void setPrecision(int prec)  
public int getSize()  
public void setSize(int size)  
public int getType()  
public void setType(int type)  
public com.ms.com.Variant getValue()  
public void setValue(Object v)  
public AdoProperties getProperties()  
```  
  
## <a name="parameter-accessor-methods"></a>Parameter-Zugriffsmethoden  
 Die [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft von einem [Parameter](../../../ado/reference/ado-api/parameter-object.md) Objekt ruft ab oder legt den Inhalt dieses Objekts fest. Der Inhalt wird als eine Variante, eine Art von Objekt, das ein Wert zugewiesen werden kann und verschiedene Datentypen dargestellt.  
  
 ADO/WFC implementiert die **Wert** Eigenschaft mit dem **GetValue** Methode, die einen VARIANT-Objekt zurückgibt und die **SetValue** Methode, die einen Variant-Wert als Argument akzeptiert. Varianten sind sehr effizient in bestimmten Sprachen, z. B. Microsoft Visual Basic.  
  
 Zusätzlich zu den **Wert** Eigenschaft ADO/WFC bietet *Accessor* Methoden, die mit Java-Datentypen abrufen und Festlegen des Inhalts von **Parameter** Objekte. Die meisten dieser Methoden haben Namen im Format **abrufen***DataType* oder **festgelegt***DataType*.  
  
 Eine wichtige Ausnahme besteht: besteht keine **GetNull** Eigenschaft; stattdessen wird ein **IsNull** -Eigenschaft, die einen booleschen Wert, der angibt, ob das Feld null zurückgibt.  
  
```  
public boolean getBoolean()  
public void setBoolean(boolean v)  
public byte getByte()  
public void setByte(byte v)  
public double getDouble()  
public void setDouble(double v)  
public float getFloat()  
public void setFloat(float v)  
public int getInt()  
public void setInt(int v)  
public long getLong()  
public void setLong(long v)  
public short getShort()  
public void setShort(short v)  
public String getString()  
public void setString(String v)  
public boolean isNull()  
public void setNull()  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Parameter-Objekt](../../../ado/reference/ado-api/parameter-object.md)
