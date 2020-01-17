# ES6.5
Study and Job ES6.5(Elasticsearch 6.5)
- ES의 구조
Index(Database)<br>
|-- Type(Table)<br>
    |--documents(row)<br>
       |--Fields<br>
       |-- Fields<br>
       |-- Fields<br>
    |-- documents(row)<br>
    |-- documents(row)<br>

- ES는 RESTful 형식을 사용한다.

# Index(색인, Indices API)
## 데이터를 저장할 테이블의 구조 정의
- 정의 : Create Index
- 형식 : 
        ```C
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
            
```C
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
# Mapping(맴핑)
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
