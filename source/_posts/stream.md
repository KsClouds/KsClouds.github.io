---
title: stream
date: 2020-06-09 23:24:52
tags: [java, lambda, resource]
cover: http://p1.hoopchina.com.cn/personPic/78e9db62-9ac3-4710-9364-113972d42c5e.jpg
---

### list to map
```java
// before
Map<String, List<AutoTemplateParamInstant>> instanceIdTemplateParamInstantsMap = new HashMap<>();
ListUtil.nvlList(autoMapper.queryAutoTemplateParamInstantByIds(instanceIdList)).stream().forEach(autoTemplateParamInstant -> {
    if (instanceIdTemplateParamInstantsMap.containsKey(autoTemplateParamInstant.getInstanceId())) {
        instanceIdTemplateParamInstantsMap.get(autoTemplateParamInstant.getInstanceId()).add(autoTemplateParamInstant);
    } else {
        instanceIdTemplateParamInstantsMap.put(autoTemplateParamInstant.getInstanceId(), ListUtil.asList(autoTemplateParamInstant));
    }
});
// after
Map<String, List<AutoTemplateParamInstant>> instanceIdTemplateParamInstantsMap = ListUtil.nvlList(autoMapper.queryAutoTemplateParamInstantByIds(instanceIdList))
    .stream().collect(Collectors.toMap(AutoTemplateParamInstant::getInstanceId, autoTemplateParamInstant -> ListUtil.asList(autoTemplateParamInstant),
        ListUtil::mergeList));
// util
public static <T, U> Map<String, List<U>> list2Map(List<T> list, Function<? super T, String> keyMapper,
                                                Function<? super T, ? extends List<U>> valueMapper) {
    return nvlList(list).stream().collect(Collectors.toMap(keyMapper, valueMapper, ListUtil::mergeList));
}
// use util
Map<String, List<AutoInstanceTemplatePosShow>> posShowAllMap = ListUtil.list2Map(autoMapper.queryPosShowByTemplateIds(templateIdList),
        AutoInstanceTemplatePosShow::getTemplateId, ListUtil::asList);
Map<String, List<String>> posShowMap = ListUtil.list2Map(autoMapper.queryPosShowByInstanceIds(instanceIdList),
        AutoInstanceTemplatePosShow::getInstanceId, posShow -> ListUtil.asList(posShow.getPosTemplateId()));
```

### map to list
```java
map.values().stream().collect(Collectors.toList());
```