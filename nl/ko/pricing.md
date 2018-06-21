---

copyright:
  years: 2016,2018
lastupdated: "2018-01-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 가격 책정
{: #pricing}

## 기본 구성
{{site.data.keyword.composeForRedis_full}} 서비스는 각각 256MB의 메모리와 256MB의 스토리지가 있는 Redis Sentinel 노드로 시작되며, 이는 리소스 1개 단위와 동일합니다. 이 서비스는 복제 및 고가용성 기능을 _포함_하므로 각 단위 및 단위당 가격은 두 노드 전체에 있는 리소스의 비용을 _포함_합니다.

기본 구성은 복제 처리를 위한 전용 Sentinel 노드와 연결 관리를 위한 HAProxy 포털 또한 포함합니다. Sentinel 노드와 HAProxy 포털에는 각각 64MB의 메모리가 있습니다.

### 비용
기본 서비스 구성에는 설정된 가격이 있습니다. 사용자의 지역 통화로 되어 있는 기본 가격 책정은 {{site.data.keyword.cloud_notm}}의 카탈로그 타일을 참조하십시오. 예를 들면, 기본 가격은 US 달러로 $13/월입니다.

## 확장 옵션
서비스에 대해 추가 메모리가 필요한 경우에는 1:1의 디스크 스토리지 대 메모리 단위로 할당되는 리소스를 늘릴 수 있습니다. {{site.data.keyword.composeForRedis}} 단위는 256MB의 스토리지와 256MB의 메모리로 구성되어 있으며, 각 단위 및 단위당 가격은 두 노드 전체의 리소스를 늘리는 비용을 _포함_합니다.

### 비용
각 추가 단위(256MB 스토리지/256MB 메모리)에는 단위당 가격이 있으며, 이는 서비스에 대한 {{site.data.keyword.cloud_notm}} 카탈로그 타일에 사용자의 지역 통화로 나열되어 있습니다. 각 추가 단위 비용은 US 달러로 $13입니다. 아래 단계별 가격 책정 표에 표시되어 있는 바와 같이, 사용자의 _총_ {{site.data.keyword.composeForRedis}} 서비스 크기가 증가하면 단위당 가격은 감소합니다.

### 단계별 가격 책정
단위 수|단위당 가격
----------|-----------
1 - 9개 단위|기본 단위당 가격 -- $13.00 USD/단위
10 - 24개 단위|10% 감소 -- $11.70 USD/단위
25 - 49개 단위|20% 감소 -- $10.40 USD/단위
50 - 99개 단위|30% 감소 -- $9.10 USD/단위
100 - 499개 단위|40% 감소 -- $7.80 USD/단위
500 - 999개 단위|50% 감소 -- $6.50 USD/단위
1,000 - 4,999개 단위|60% 감소 -- $5.20 USD/단위
5,000개 이상 단위|70% 감소 -- $3.90 USD/단위
{: caption="표 1. {{site.data.keyword.composeForRedis}} 단계별 가격 책정" caption-side="top"}
