---
title: Feld (ADO - WFC-Syntax) | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 02/15/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Field collection [ADO], ADO/WFC syntax
ms.assetid: 7e01cb24-2338-4f92-ad46-8d97248e1a4d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ea83e9a9d928ebfbab416a6cf85b4adbc887f05
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="field-ado---wfc-syntax"></a>Feld (ADO - WFC-Syntax)
## <a name="package-commswfcdata"></a>Paket com.ms.wfc.data  
  
### <a name="methods"></a>Methoden  
  
```  
public void appendChunk(byte[] bytes)  
public void appendChunk(char[] chars)  
public void appendChunk(String chars)  
public byte[] getByteChunk(int len)  
public char[] getCharChunk(int len)  
public String getStringChunk(int len)  
```  
  
### <a name="properties"></a>Eigenschaften  
  
```  
public int getActualSize()  
public int getAttributes()  
public void setAttributes(int pl)  
public com.ms.com.IUnknown getDataFormat()  
public void setDataFormat(com.ms.com.IUnknown format)  
```  
  
 (Weitere Informationen finden Sie in der Dokumentation für die com.ms.wfc.data.IDataFormat-Schnittstelle.)  
  
```  
public int getDefinedSize()  
public void setDefinedSize(int pl)  
public String getName()  
public int getNumericScale()  
public void setNumericScale(byte pbNumericScale)  
public Variant getOriginalValue()  
public int getPrecision()  
public void setPrecision(byte pbPrecision)  
public int getType()  
public void setType(int pDataType)  
public Variant getUnderlyingValue()  
public Variant getValue()  
public void setValue(Variant value)  
public AdoProperties getProperties()  
```  
  
### <a name="field-accessor-methods"></a>Feld-Zugriffsmethoden  
 Die [Wert](../../../ado/reference/ado-api/value-property-ado.md) Eigenschaft von einem [Feld](../../../ado/reference/ado-api/field-object.md) Objekt ruft ab oder legt den Inhalt dieses Objekts fest. Der Inhalt wird als eine Variante, eine Art von Objekt, das ein Wert zugewiesen werden kann und verschiedene Datentypen dargestellt.  
  
 ADO/WFC implementiert die **Wert** Eigenschaft mit dem **GetValue** Methode, die einen VARIANT-Objekt zurückgibt und die **SetValue** Methode, die einen Variant-Wert als Argument akzeptiert. Varianten sind sehr effizient in bestimmten Sprachen, z. B. Microsoft Visual Basic.  
  
 Zusätzlich zu den **Wert** Eigenschaft ADO/WFC bietet *Accessor* Methoden, die mit Java-Datentypen abrufen und Festlegen des Inhalts von **Feld** Objekte. Die meisten dieser Methoden haben Namen im Format **abrufen***DataType* oder **festgelegt***DataType*.  
  
 Es gibt zwei wichtige Ausnahmen: eines der **GetObject** Methoden gibt ein Objekt in einer bestimmten Klasse umgewandelt. Ist keine **GetNull** Eigenschaft; stattdessen wird ein **IsNull** -Eigenschaft, die einen booleschen Wert, der angibt, ob das Feld null zurückgibt.  
  
```  
public native boolean getBoolean();  
public void setBoolean(boolean v)  
public native byte getByte();  
public void setByte(byte v)  
public native byte[] getBytes();  
public void setBytes(byte[] v)  
public native double getDouble();  
public void setDouble(double v)  
public native float getFloat();  
public void setFloat(float v)  
public native int getInt();  
public void setInt(int v)  
public native long getLong();  
public void setLong(long v)  
public native short getShort();  
public void setShort(short v)  
public native String getString();  
public void setString(String v)  
public native boolean isNull();  
public void setNull()  
public Object getObject()  
public Object getObject(Class c)  
public void setObject(Object value)  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Field-Objekt](../../../ado/reference/ado-api/field-object.md)

