---
title: Перечисление CorPropertyAttr
ms.date: 03/30/2017
api_name:
- CorPropertyAttr
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- CorPropertyAttr
helpviewer_keywords:
- CorPropertyAttr enumeration [.NET Framework metadata]
ms.assetid: 58ac8202-854d-4efd-acfb-d2da8b446e12
topic_type:
- apiref
ms.openlocfilehash: 2d49a146a465210cea8466a75666ca3f800b090b
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/23/2019
ms.locfileid: "74450143"
---
# <a name="corpropertyattr-enumeration"></a>Перечисление CorPropertyAttr
Содержит значения, описывающие метаданные свойства.  
  
## <a name="syntax"></a>Синтаксис  
  
```cpp  
typedef enum CorPropertyAttr {  
  
    prSpecialName           =   0x0200,   
    prReservedMask          =   0xf400,  
    prRTSpecialName         =   0x0400,  
    prHasDefault            =   0x1000,  
    prUnused                =   0xe9ff  
  
} CorPropertyAttr;  
```  
  
## <a name="members"></a>Члены  
  
|Член|Описание|  
|------------|-----------------|  
|`prSpecialName`|Указывает, что свойство является специальным, и что его имя описывает, как это делать.|  
|`prReservedMask`|Зарезервировано для внутреннего использования средой CLR.|  
|`prRTSpecialName`|Указывает, что внутренние API метаданных среды CLR должны проверять кодировку имени свойства.|  
|`prHasDefault`|Указывает, что свойство имеет значение по умолчанию.|  
|`prUnused`|Не используется.|  
  
## <a name="requirements"></a>Требования  
 **Платформы:** см. раздел [Требования к системе](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Заголовок:** Корхдр. h  
  
 **Версии платформы .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>См. также

- [Перечисления метаданных](../../../../docs/framework/unmanaged-api/metadata/metadata-enumerations.md)
