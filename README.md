# 중고차 검색 데이터셋 (Used Car Search Dataset)

이 데이터셋은 Elasticsearch의 Bulk API를 사용하여 색인하기 위해 준비된 중고차 매물 데이터입니다.

## 파일 정보
- **파일명**: `search-used-car.json`
- **데이터 개수**: 100,000건
- **형식**: NDJSON (Newline Delimited JSON) - Elasticsearch Bulk 포맷

## 데이터 구조
각 문서는 Elasticsearch `search-used-car` 인덱스에 색인되도록 구성되어 있습니다.

데이터는 메타데이터 라인과 소스 데이터 라인이 번갈아 나타나는 형태로 구성되어 있습니다.

```json
{"index":{"_index":"search-used-car","_id":"7315142473"}}
{"id":"7315142473", "brand":"도요타", "model":"tundra", "price":11995, ...}
```

## 주요 필드 설명

| 필드명 | 타입 | 설명 | 예시 |
|---|---|---|---|
| `id` | Keyword | 매물 고유 ID | `"7315142473"` |
| `url` | Keyword | 원본 게시글 URL | `"https://..."` |
| `region` | Keyword | 지역 명 | `"maine"`, `"delaware"` |
| `region_url` | Keyword | 지역 URL | `"https://..."` |
| `price` | Integer | 가격 (USD) | `11995` |
| `year` | Integer | 연식 | `2008` |
| `manufacturer` | Keyword | 제조사 (영문) | `"toyota"`, `"hyundai"` |
| `model` | Text | 모델명 | `"tundra"`, `"sonata"` |
| `condition` | Keyword | 차량 상태 | `"excellent"`, `"good"` |
| `cylinders` | Keyword | 기통 수 | `"6 cylinders"`, `"4 cylinders"` |
| `fuel` | Keyword | 연료 타입 | `"gas"`, `"hybrid"` |
| `odometer` | Integer | 주행 거리 (마일) | `136000` |
| `title_status` | Keyword | 소유권 상태 | `"clean"`, `"rebuilt"` |
| `transmission` | Keyword | 변속기 | `"automatic"` |
| `drive` | Keyword | 구동 방식 | `"4wd"`, `"fwd"` |
| `size` | Keyword | 차량 크기 | `"full-size"`, `"compact"` |
| `type` | Keyword | 차량 유형 | `"pickup"`, `"sedan"`, `"SUV"` |
| `paint_color` | Keyword | 색상 | `"blue"`, `"grey"` |
| `image_url` | Keyword | 이미지 URL | `https://...` |
| `country` | Keyword | 국가 | `"USA"` |
| `state` | Keyword | 주 (State) | `"me"`, `"de"` |
| `lat` | Float | 위도 | `43.188725` |
| `lng` | Float | 경도 | `-71.50493` |
| `posting_date` | Date | 게시 일자 | `"2021-04-30T21:52:02-0400"` |
| `brand` | Text | 브랜드 (한글) | `"도요타"`, `"현대"` |
| `timeStamp` | Date | 데이터 생성 시간 | `"2022-07-10 11:47:10"` |
| `vin` | Keyword | 차대 번호 | `"5TFRU54178X014539"` |

## 사용 방법 (Usage)

Elasticsearch에 이 데이터를 Bulk Indexing 하려면 다음 명령어를 사용할 수 있습니다.

```bash
curl -H "Content-Type: application/x-ndjson" -XPOST "localhost:9200/_bulk" --data-binary "@search-used-car.json"
```

> **참고**: `search-used-car.json` 파일의 용량이 크므로(약 72MB), `data-binary` 옵션을 사용하는 것이 좋습니다.
