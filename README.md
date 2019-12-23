# ES6.5
Study and Job ES6.5(Elasticsearch 6.5)
- ES의 구조
Index(Database)
\t|-- Type(Table)<br>
\t\t|-- documents(row)<br>
\t\t\t|-- Fields<br>
\t\t\t\t|-- Fields<br>
\t\t\t\t\t|-- Fields<br>
\t\t\t\t|-- documents(row)<br>
\t\t\t\t|-- documents(row)<br>

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
# Search(검색)
# Aggregations(통계)
## SQL의 GROUP BY 와 같이 데이터를 그룹화하고 통계(Agg)를 얻는 기능.
- ES는 **검색과 동시에 집계(통계) 결과**를 반환할 수 있다. **집계만 표시하려면 size: 0**
