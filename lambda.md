## 分组 替换
```java
List<String> positionIds = r1.stream().filter(r->StringUtil.hasText(r.getPositionId())).map(UserOwnerPosition::getPositionId).distinct().collect(Collectors.toList());
				List<Position> ps = positionService.getByIds(positionIds);
				Map<String,Position> ref = ps.stream().collect(Collectors.toMap(Position::getId, r->r));
				
				Map<String, List<Position>>  result = r1.stream().filter(r->ref.containsKey(r.getPositionId()))
						.map(r->{
							return new TwoTuple<String, Position>(r.getOwnerId(), ref.get(r.getPositionId()));
				}).collect(Collectors.groupingBy(r->r.a,Collectors.mapping(r->r.b,Collectors.toList())));
				

```
