### PostgreSQL vs MySQL ??

# MySQL vs PostgreSQL

## ACID 규정 준수

- 원자성, 일관성, 격리성, 지속성(ACID)은 예상치 못한 오류가 발생한 후에도 데이터베이스를 유효한 상태로 유지하는 데이터베이스 속성. 예를 들어, 많은 수의 행을 업데이트했는데 중간에 시스템이 실패하는 경우 행을 수정해서는 안됨.

  

MySQL은 InnoDB 및 NDB 클러스터 스토리지 엔진 또는 소프트웨어 모듈과 함께 사용하는 경우에만 ACID 규정 준수를 제공

  

PostgreSQL은 모든 구성에서 ACID와 완벽하게 호환

  

## 동시성 제어

- 다중 버전 동시성 제어(MVCC)는 레코드의 중복 사본을 생성하여 동일한 데이터를 병렬로 안전하게 읽고 업데이트하는 고급 데이터베이스 기능임. MVCC를 사용하면 여러 사용자가 데이터 무결성을 손상시키지 않고 동일한 데이터를 동시에 읽고 수정할 수 있음.

  

MySQL 데이터베이스는 MVCC를 제공 X

  

PostgreSQL은 이 기능을 지원 O

  

## **인덱스**

- 데이터베이스는 인덱스를 사용하여 데이터를 더 빠르게 검색함. 자주 액세스하는 데이터를 다른 데이터와 다르게 정렬 및 저장하도록 데이터베이스 관리 시스템을 구성하여 자주 액세스하는 데이터를 인덱싱할 수 있음.

  

MySQL은 계층적으로 인덱싱된 데이터를 저장하는 B-트리 및 R-트리 인덱싱을 지원

  

PostgreSQL 인덱스 유형에는 트리, 표현식 인덱스, 부분 인덱스 및 해시 인덱스가 포함됨. 크기를 확장할 때 데이터베이스 성능 요구 사항을 세밀하게 조정할 수 있는 더 많은 옵션이 있음.

  

## **데이터 유형**

MySQL은 순수 관계형 데이터베이스

  

반면 PostgreSQL은 객체 관계형 데이터베이. 즉, PostgreSQL에서는 데이터를 속성을 가진 객체로 저장할 수 있음. 객체는 Java 및 .NET과 같은 여러 프로그래밍 언어의 일반적인 데이터 유형임. 객체는 상위-하위 관계 및 상속과 같은 패러다임을 지원함. PostgreSQL을 사용하는 것은 데이터베이스 개발자에게 더 직관적임. PostgreSQL은 배열 및 XML과 같은 다른 추가 데이터 유형도 지원함.

  

## **저장 프로시저**

- 저장 프로시저는 미리 작성하고 저장할 수 있는 구조화된 쿼리 언어(SQL) 쿼리 또는 코드 명령문임. 동일한 코드를 반복해서 재사용할 수 있으므로 데이터베이스 관리 작업이 더 효율적.

  

MySQL과 PostgreSQL 모두 저장 프로시저를 지원하지만

PostgreSQL을 사용하면 SQL 이외의 언어로 작성된 저장 프로시저를 호출할 수 있음.

  

## **트리거**

- 트리거는 데이터베이스 관리 시스템에서 관련 이벤트가 발생할 때 자동으로 실행되는 저장 프로시저.

  

MySQL 데이터베이스에서는 SQL _INSERT_, _UPDATE_ 및 _DELETE_ 문에 _AFTER_ 및 _BEFORE_ 트리거만 사용할 수 있음. 즉, 사용자가 데이터를 수정하기 전이나 후에 프로시저가 자동으로 실행됨.

  

반대로 PostgreSQL은 _INSTEAD OF_ 트리거를 지원하므로 함수를 사용하여 복잡한 SQL 문을 실행할 수 있음.

## 쓰기 성능

- MySQL은 쓰기 잠금을 사용하여 실제 동시성을 구현. 예를 들어 한 사용자가 테이블을 편집하는 경우 다른 사용자가 테이블을 변경하려면 작업이 완료될 때까지 기다려야 할 수 있음. 그러나 PostgreSQL에는 읽기-쓰기 잠금이 없는 다중 버전 동시성 제어(MVCC) 지원이 내장되어 있음. 따라서 쓰기 작업이 빈번하고 동시에 수행되는 경우 PostgreSQL 데이터베이스가 더 잘 작동함.

## 대량 데이터 처리

- PostgreSQL은 대규모 데이터셋 및 복잡한 쿼리에 대해 높은 성능과 확장성을 제공할 수 있어서 선택.
- PostgreSQL은 쓰기 작업이 빈번하고 쿼리가 복잡한 엔터프라이즈급 애플리케이션에 더 적합함.