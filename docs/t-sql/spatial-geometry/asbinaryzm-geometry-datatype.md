---
title: AsBinaryZM (Geometry-Datentyp) | Microsoft Docs
ms.custom: 
ms.date: 08/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- AsBinaryZM geometry
ms.assetid: 5eae2872-adca-4b8f-8b04-4ee91ced98f1
caps.latest.revision: 6
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e2b778d41e6a3d4f7701140584fd3c833a726948
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="asbinaryzm-geometry-datatype"></a>AsBinaryZM (geometry-Datentyp)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

Gibt die Open Geospatial Consortium (OGC) Well-Known Binary (WKB)-Darstellung einer **Geometrie** Instanz getragenen alle **Z** (Höhe) und **M** (Measure) Werte, die von der Instanz getragen werden.
  
## <a name="syntax"></a>Syntax  
  
```  
  
.AsBinaryZM()  
```  
  
## <a name="return-types"></a>Rückgabetypen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Rückgabetyp: **varbinary(max)**  
  
 CLR-Rückgabetyp: **SqlBytes**  
  
## <a name="remarks"></a>Hinweise  
  
## <a name="examples"></a>Beispiele  
  
```tsql  
DECLARE @g1 GEOMETRY = 'Point(1 1 2 3)';  
  
SELECT @g1.STAsBinary();  
-- Returns: 0x0101000000000000000000F03F000000000000F03F  
  
SELECT @g1.AsBinaryZM();  
--Returns: 0x01B90B0000000000000000F03F000000000000F03F00000000000000400000000000000840  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erweiterte Methoden für Geometry-Instanzen](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [Übe &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40; Geometry-Datentyp &#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

