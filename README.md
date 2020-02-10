# ES6.5
Study and Job ES6.5(Elasticsearch 6.5)
- ES의 구조
```sh
Index(Database)
└─ Type(Table)
   ├─ documents(row)
   │   ├─ Fields_A
   │   │  ├─ Fields_A.analyzer
   │   │  └─ Fields_A.analyzer
   │   ├─ Fields_B
   │   ├─ Fields_C
   ├─ documents(row)
   ├─ documents(row)
```
- ES는 RESTful 형식을 사용한다.

# Mapping(맴핑)
## 데이터를 저장할 테이블의 구조 정의
- 정의 : Create Mappging, 엘라스틱서치는 schemaLess 구조이다. 그래서 Mapping 설정 색인을 하더라도, 자동으로 shema가 생성된다.<br>
        하지만, 그렇게 되면 실제 운영환경에서는 색인이 안되는 경우가 발생할 수 도 있기 때문에 꼭! Mapping 정의를 한 이후에 색인을 해야한다.
- 형식 : 
```sh
PUT _INDEX_NAME/_TYPE_NAME
{
   "mappings" : {
      "TYPE_NAME" : {
         "properties" : {
            "FIELD_NAME_1" : {
               "properties" : {
                    "FIELD_NAME1-1" : {
                      "type" : "VALUE"
                    }
               }
            },
            "FIELD_NAME_2" : {
                  "type" : "VALUE"
                },
                ...
              }
            }
}        

```
- 예시 :             
```sh
PUT order
{
    "mappings": {
      "default": {
        "properties": {
          "lines": {
            "properties": {
              "amount": {
                "type": "double"
              },
              "product_id": {
                "type": "integer"
              },
              "quantity": {
                "type": "short"
              }
            }
          },
          "purchased_at": {
            "type": "date"
          },
          "sales_channel": {
            "type": "keyword"
          },
          "salesman": {
            "properties": {
              "id": {
                "type": "integer"
              },
              "name": {
                "type": "text"
              }
            }
          },
          "status": {
            "type": "keyword"
          },
          "total_amount": {
            "type": "double"
          }
        }
      }
    }
}
```
# Field Data Type
- 정의 : RDB와 마찬가지로 엘라스틱서치도 다양한 데이터 타입을 가지고 있다.
- 데이터 타입
1. keyword <br>
- 정의 : 말 그대로 키워드(keywrod) 형태로 사용할 데이터에 적합한 데이터 타입. keyword타입을 사용하는 경우 별도의 분석기를 거치지 않고 원문 그대로 색인하기 때문에 특정 코드나 키워드 등 **정형화된 콘텐츠**에 주로 사용된다.
- 특징 : **검색시 필터링되는 항목, 정렬이 필요한 항목, 집계(Aggregation)해야하는 항목**
2. text 
- 정의 : 색인 시 지정된 분석기가 컬럼의 데이터를 문자열 데이터로 인식하고 이를 분석 후 토큰화하여 색인한다.
- 특징 : **전문 검색이 가능하며, 전체 텍스트가 토큰화되어 생성되면 특정 단어를 검색하는 것이 가능해진다.**
>>> 만약 검색뿐 아니라, 정렬(Sorting)이나 집계(Aggregation)를 연산을 사용해야 할 경우 에는 **`Multi Field`***로 정의해주면된다.
3. Array
4. Numeric
5. Date
6. Object

# Template(템플릿)
# Search(검색)
# Aggregations(통계)
## SQL의 GROUP BY 와 같이 데이터를 그룹화하고 통계(Agg)를 얻는 기능.
- ES는 **검색과 동시에 집계(통계) 결과**를 반환할 수 있다. **집계만 표시하려면 size: 0**
## 구조
- ㅇㅇㅇ
```
"aggregations":{
    "<aggregation_name>":{
        "<aggregation_type>":{
            "<aggregation_body>"
        }
        [,"meta":{[<meta_data_body>]}]?
        [,"aggregations":{[<sub_aggregation>]+}]?
    }
    ,[,"<aggregation_name_2>:{...}"]*
}
```


## 데이터 집계 타입
- 데이터 집계 타입은 다음과 같이 4가지가 존재합니다.
1. 버킷 집계(Bucket Aggregation)
문서의 필드 기준으로 버킷을 집계합니다.
2. 매트릭 집계(Metric Aggregation)
문서에서 추출된 값을 이용하여 합계, 최대값, 최소값, 평균값 등을 계산합니다.

3. 매트릭스 집계(Matrix Aggregation)
행렬 값을 합하거나 곱합니다.

4.파이프라인 집계(Pipeline Aggregation)
일반적 파이프라인의 개념으로 집계에 의해 생성된 집계 결과를 이용해 또 다시 집계합니다.
